<template>
  <div class="notes">
    <div class="container">
      <div class="notes__top">
        <h2 class="notes__title">{{ notes.length > 0 ? words.infobar[lang] : words.noinfobar[lang]}}</h2>
        <button class="notes__btn" @click="grid = !grid">
          <img src="@/assets/img/list.svg" alt="list" v-if="grid" />
          <img src="@/assets/img/grid.svg" alt="list" v-else />
          <span>{{ grid ? words.list[lang] : words.grid[lang] }}</span>
        </button>
      </div>
      <div class="notes__list" :class="{ active: !grid }">
        <NoteItem
          :lang="lang"
          :grid="grid"
          v-for="note in notes"
          :key="note.id"
          :note="note"
          @changeNote="$emit('changeNote', note.id)"
          @delNote="$emit('delNote', note.id)"
        />
      </div>
    </div>
  </div>
</template>

<script>
import NoteItem from "@/components/NoteItem.vue";
export default {
  components: {
    NoteItem,
  },
  data() {
    return {
      grid: true,
    };
  },
   inject: ['words'],
  props: {
    lang:String,
    notes: {
      typeof: Array,
      required: true,
    },
  },
};
</script>

<style>
.notes {
  margin-top: 30px;
}
.notes__top {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.notes__title {
  font-size: 22px;
  line-height: 28px;
  color: #323232;
}
.notes__btn {
  background: linear-gradient(
      0deg,
      rgba(103, 80, 164, 0.11),
      rgba(103, 80, 164, 0.11)
    ),
    #fffbfe;
  box-shadow: 0px 4px 8px 3px rgba(0, 0, 0, 0.15),
    0px 1px 3px rgba(0, 0, 0, 0.3);
  border-radius: 16px;
  width: 120px;
  height: 56px;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 15px;
}
.notes__btn span {
  letter-spacing: 0.1px;
  color: #6750a4;
  font-size: 14px;
  line-height: 20px;
  font-family: "RM";
}
.notes__list {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
  margin-top: 50px;
}
.notes__list.active {
  grid-template-columns: 1fr;
}
</style>