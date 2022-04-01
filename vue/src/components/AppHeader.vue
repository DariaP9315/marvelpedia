<template>
  <header class="header">
    <img src="../../../image/Marvel_Logo.svg" alt="logo" class="header__logo" />
    <form class="header__search">
      <input
        class="searchfield"
        type="text"
        placeholder="what are you finding?"
        v-model="search"
        @input="changeSearch(search)"
      />
      <button class="search__submit" type="submit"></button>
    </form>
  </header>
</template>

<script>
export default {
  name: 'AppHeader',
  props: ['changeSearch'],
  data() {
    return {
      search: '',
    };
  },
};
</script>

<style scoped>
.header {
  background-color: rgb(36, 35, 35);

  height: 60px;
  margin: 0 auto;
  color: #fff;
  font-family: Arial, Helvetica, sans-serif;
  display: flex;
  justify-content: space-between;
  padding-left: 15px;
  padding-right: 15px;
}
.header__logo {
  width: 100px;
  align-self: center;
}

.header__search {
  display: flex;
  align-self: center;
}

.search__submit {
  box-sizing: border-box;
  border: none;
  border-radius: 5px;
  background-image: url('../../../image/icon-search.svg');
  background-color: #fff;
  background-position: center;
  background-size: 15px 15px;
  background-repeat: no-repeat;
  width: 25px;
  height: 25px;
  padding: 0;
  margin-left: 10px;
  align-self: center;
}

.searchfield {
  box-sizing: border-box;
  border: none;
  border-radius: 5px;
  padding: 0;
  padding-left: 10px;
  margin: 0;
}
</style>
