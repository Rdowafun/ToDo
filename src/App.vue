<template>
  <Navbar
  @searchValue = "search = $event"
  :lang="lang"
  @changeLang="changeLang"
  />
  <Notes
  :lang="lang"
  :notes = "filterNotes"
  @delNote = "deleteNote"
  @changeNote = "changeNote"
  :search = "search"
  />
  <Modal
  :lang="lang"
  :edit = "edit"
  :editNote = "editNote"
  :currentId="currentId"
   v-show="modalOpen"
   @closeModal="closeModal"
   @addNote="addNote"
   @editedNote="editedNote"
   />
  <AddButtons @openModal="openModal" />
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import Notes from "@/components/Notes.vue";
import Modal from "@/components/Modal.vue";
import AddButtons from "@/components/AddButtons.vue";
import langs from '@/lang'

export default {
  components: {
    Navbar,
    Notes,
    Modal,
    AddButtons,
  },
  data() {
    return {
      currentId: 1,
      modalOpen: false,
      notes: [],
      edit:false,
      editNote:{},
      search: '',
      lang:'ru',
      langwords:{},
    };
  },
  created(){
    this.getNotes();
    localStorage.lang = localStorage.lang || 'ru';
    this.lang = localStorage.lang || 'ru';
    this.langwords = langs;
    localStorage.words = JSON.stringify(this.langwords)
  },
  computed:{
    filterNotes(){
      return this.search ? this.notes.filter(note=> note.title.toLowerCase().includes(this.search.toLowerCase())) : this.notes;
    }
  },
  provide(){
    return{
      words: langs || JSON.parse(localStorage.words)
    }
  },
  methods: {
    openModal() {
      this.modalOpen = true;
    },
    closeModal(status) {
      this.modalOpen = status;
      setTimeout(()=> this.edit = false, 500);
    },
    addNote(item){
    this.notes.push(item);
    this.modalOpen = false;
    },
    deleteNote(id){
      let index = this.notes.findIndex(note => note.id == id)
      this.notes.splice(index, 1)
    },
    getNotes(){
      const localNotes = localStorage.notes
      if(localNotes){
        this.notes = JSON.parse(localNotes)
      }
    },
    changeNote(id){
      this.edit = this.modalOpen = true;
      let pickedNote = this.notes.find(note => note.id == id);
      this.editNote = pickedNote
    },
    editedNote(noteEdited){
      this.notes.forEach(note=>{
        if(note.id == noteEdited.id){
          note.title = noteEdited.title;
          note.descr = noteEdited.descr;
          note.date = noteEdited.date;
        }
      })
    },
    changeLang(val){
      this.lang = localStorage.lang = val;
    }
  },
  watch:{
    notes:{
      handler(newNotes){
        localStorage.notes = JSON.stringify(this.notes)
      },
      deep: true
    }
  }
};
</script>

<style>
</style>
