<template>
  <div class="notes__item">
    <div class="notes__item-top" :class="{ between: !grid }">
      <h3 class="notes__item-title">{{ note.title }}</h3>
      <p class="notes__item-date">{{ note.date }}</p>
    </div>
    <p class="notes__item-text">{{ note.descr }}</p>
    <div class="notes__item-btns">
      <button class="notes__item-btn edit" @click="$emit('changeNote', note.id)">
        <img src="@/assets/img/edit.svg" alt="edit" />
        <span>{{words.editbtn[lang]}}</span>
      </button>
      <button class="notes__item-btn del" @click="$emit('delNote', note.id)">
        <img src="@/assets/img/del.svg" alt="del" />
        <span>{{words.deledit[lang]}}</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  inject: ['words'],
  props: {
    lang:String,
    grid: Boolean,
    note: Object,
  },
};
</script>

<style>
.notes__item {
  background: linear-gradient(
      0deg,
      rgba(103, 80, 164, 0.05),
      rgba(103, 80, 164, 0.05)
    ),
    #fffbfe;
  box-shadow: 0px 1px 2px rgba(0, 0, 0, 0.3),
    0px 1px 3px 1px rgba(0, 0, 0, 0.15);
  border-radius: 16px;
  padding: 16px 16px 28px 16px;
}
.notes__item-title {
  font-family: "RM";
  font-size: 16px;
  line-height: 24px;
  letter-spacing: 0.1px;
  color: #1c1b1f;
}
.notes__item-date {
  font-size: 14px;
  line-height: 20px;
  letter-spacing: 0.25px;
  color: #cac4d0;
}
.notes__item-text {
  font-size: 14px;
  line-height: 20px;
  letter-spacing: 0.25px;
  color: #49454f;
  margin: 15px 0 30px 0;
}
.notes__item-btns {
  display: flex;
  justify-content: flex-end;
  gap: 17px;
  align-items: center;
}
.notes__item-btn {
  display: flex;
  align-items: center;
  gap: 10px;
  background: transparent;
  color: #6750a4;
  padding: 12px;
  border-radius: 5px;
  transition: 200ms ease-in-out;
}
.notes__item-btn span {
  font-size: 14px;
  font-family: "RM";
  line-height: 20px;
  letter-spacing: 0.1px;
  text-transform: uppercase;
}
.edit {
  color: #6750a4;
}
.edit:hover {
  background: #e6ddff;
}
.del {
  color: #cf1b1b;
}
.del:hover {
  background: #ffe1e1;
}
.between {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
</style>