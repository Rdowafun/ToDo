<template>
  <Transition name="modal">
    <div class="modal" @click="closeModal">
      <div class="modal__block" @click.stop="">
        <h2 class="modal__title">
          {{edit ? words.titlewindowedit[lang] : words.titlewindow[lang] }}
        </h2>
        <div class="modal__inputs">
          <label>
            <span>Title</span>
            <input type="text" v-model="title" />
          </label>
          <label>
            <span>Content</span>
            <textarea v-model="descr"></textarea>
          </label>
        </div>
        <div class="modal__btns">
          <button class="modal__btn del" @click="closeModal">{{words.closebtn[lang]}}</button>
          <button v-if="!edit" class="modal__btn edit" @click="addNote">{{words.addbtn[lang]}}</button>
          <button v-else class="modal__btn edit" @click="changeNote">{{words.editwindowbtn[lang]}}</button>
        </div>
      </div>
    </div>
  </Transition>
</template>

<script>
export default {
  data() {
    return {
      title: "",
      descr: "",
      id: this.currentId,
    };
  },
  inject:['words'],
  props: {
    lang:String,
    currentId: Number,
    edit: Boolean,
    editNote: Object,
  },
  methods: {
    closeModal() {
      this.$emit("closeModal", false);
      this.title = "";
      this.descr = "";
    },
    addNote() {
      if (this.title != "" && this.descr != "") {
        const item = {
          id: this.id++,
          title: this.title,
          descr: this.descr,
          date: new Date().toLocaleDateString(),
        };
        this.$emit("addNote", item);
        this.title = "";
        this.descr = "";
      }
    },
    changeNote(){
  if (this.title != "" && this.descr != "") {
    const editedNote = {
      id: this.editNote.id,
      title: this.title,
      descr: this.descr,
      date: new Date().toLocaleDateString(),
    }
    this.$emit('editedNote', editedNote);
    this.closeModal()
  }
    },
  },
};
</script>

<style>
.modal {
  background: rgba(0, 0, 0, 0.35);
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 999;
  display: flex;
  align-items: center;
  justify-content: center;
}
.modal__block {
  background: linear-gradient(
      0deg,
      rgba(103, 80, 164, 0.11),
      rgba(103, 80, 164, 0.11)
    ),
    #fffbfe;
  border-radius: 28px;
  max-width: 312px;
  width: 100%;
  padding: 24px;
}
.modal__title {
  font-size: 24px;
  line-height: 32px;
  color: #1c1b1f;
  margin-bottom: 16px;
}
.modal__inputs {
  display: flex;
  flex-direction: column;
  gap: 16px;
}
.modal__inputs label {
  position: relative;
}
.modal__inputs span {
  position: absolute;
  left: 16px;
  top: 8px;
  font-size: 12px;
  line-height: 16px;
  letter-spacing: 0.4px;
  color: #6750a4;
}
.modal__inputs input,
.modal__inputs textarea {
  background: #e7e0ec;
  border-radius: 4px 4px 0px 0px;
  resize: none;
  width: 100%;
  padding: 23px 0 9px 16px;
  font-size: 16px;
  line-height: 24px;
  letter-spacing: 0.5px;
  color: #49454f;
  border-bottom: 1px solid #1c1b1f;
}
.modal__btns {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  gap: 8px;
  margin-top: 25px;
}
.modal__btn {
  font-size: 14px;
  font-family: "RM";
  padding: 10px 12px;
  line-height: 20px;
  letter-spacing: 0.1px;
  text-transform: uppercase;
  background: transparent;
  transition: 200ms ease-in-out;
}
.modal-enter-active,
.modal-leave-active {
  transition: linear 0.2s;
}

.modal-enter-from,
.modal-leave-to {
  opacity: 0;
  transform: scale(1.5);
}
</style>