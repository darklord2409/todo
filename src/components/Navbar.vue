<template>
  <header class="header">
    <Transition name="header__notes">
      <div class="header__notes" v-show="header === true">
        <button @click="changeLang" class="header__lang" v-if="lang == 'ru'">UZ</button>
        <button @click="changeLang" class="header__lang" v-else>RU</button>
        <h1 class="header__title">{{ words.appbartitle[lang] }}</h1>
        <button class="header__search" @click="header = false">
          <img src="@/assets/img/search.svg" alt="" />
        </button>
      </div>
    </Transition>
    <Transition name="header__form">
      <div class="header__form" v-show="header === false">
        <button class="header__back" @click="(header = true), (search = '')">
          <img src="@/assets/img/arrow.svg" alt="" />
        </button>
        <input
          type="text"
          class="header__input"
          placeholder="Поиск..."
          v-model="search"
        />
        <button class="header__close" @click="search = ''">
          <img src="@/assets/img/back.svg" alt="" />
        </button>
      </div>
    </Transition>
  </header>
</template>

<script>
export default {
  data() {
    return {
      header: true,
      search: "",
    };
  },
  inject: ['words'],
  props: ['lang'],
  watch: {
    search(val){
      this.$emit('searchValue', val)
    }
  },
  methods:{
    changeLang(){
      this.$emit('changeLang', this.lang == 'ru' ? 'uz' : 'ru')
    }
  }
};
</script>

<style>
.header {
  background: #f3edf7;
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25), 0px 1px 3px rgba(0, 0, 0, 0.3);
  padding: 18px 20px;
  height: 70px;
  overflow: hidden;
}
.header__notes,
.header__form {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.header__lang {
  font-size: 24px;
  font-weight: 700;
}
.header__title {
  font-size: 22px;
  line-height: 28px;
  color: #1c1b1f;
}
.header__input {
  border: none;
  outline: none;
  width: 90%;
  background: transparent;
  font-size: 16px;
  line-height: 20px;
  color: #9d9d9d;
}

.header__notes-enter-active,
.header__notes-leave-active {
  transition: 0.5s linear;
}

.header__notes-enter-from,
.header__notes-leave-to {
  opacity: 0;
  transform: translateY(-300px);
}
.header__notes-enter-to,
.header__notes-leave-from {
  opacity: 1;
  transform: translateY(0);
}
.header__form-enter-active,
.header__form-leave-active {
  transition: 0.5s linear;
}

.header__form-enter-from,
.header__form-leave-to {
  opacity: 0;
  transform: translateY(300px);
}
.header__form-enter-to,
.header__form-leave-from {
  opacity: 1;
  transform: translateY(0);
}

</style>