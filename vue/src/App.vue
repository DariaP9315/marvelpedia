<template>
  <div id="app">
    <app-header :changeSearch="changeSearch" />

    <div class="content">
      <app-modal
        v-show="showModal"
        @close-modal="showModal = false"
        :character="searchCharacters[characterIndex]"
      />

      <div class="cards">
        <h2 class="cards__title">Персонажи Marvel</h2>
        <spinner v-if="loading" />
        <div class="cards__container">
          <div class="character" v-for="(el, idx) in searchCharacters" :key="el.id">
            <img class="card__img" :src="el.thumbnail" :alt="el.name" />
            <div class="card__info">
              <h5 class="card__name">{{ el.name }}</h5>
              <button class="card__btn" @click="(showModal = true), (characterIndex = idx)">
                Подробнее
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Spinner from './components/Spinner';
import AppModal from './components/AppModal';
import AppHeader from './components/AppHeader';

export default {
  name: 'App',
  components: {
    AppHeader,
    AppModal,
    Spinner,
  },
  data() {
    return {
      loading: false,
      characters: [],
      characterIndex: 0,
      showModal: false,
      search: '',
    };
  },
  methods: {
    fetchCharacters: function() {
      return fetch('https://netology-api-marvel.herokuapp.com/characters')
        .then((res) => res.json())
        .then((json) => (this.characters = json));
    },
    changeSearch: function(value) {
      this.search = value;
    },
  },
  computed: {
    searchCharacters: function() {
      const { search, characters } = this;
      return characters.filter(
        (character) => {
          return character.name.toLowerCase().indexOf(search.toLowerCase()) !== -1;
        },
        //character.name.toLowerCase().includes(value.toLowerCase()),
      );
    },
  },
  async mounted() {
    this.loading = true;
    await this.fetchCharacters();
    this.loading = false;
  },
};
</script>

<style>
.content {
  max-width: 100vw;
  margin: 0 auto;
}
.cards {
  margin: 30px auto;

  max-width: 1200px;
  padding-left: 20px;
  padding-right: 20px;
}

.cards__title {
  font-size: 40px;
  font-weight: 500;
  margin-bottom: 30px;
}

.cards__container {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
  gap: 17px;
}

.character {
  display: flex;
  max-width: 350px;
  border: 1px solid rgba(0, 0, 0, 0.5);
  border-radius: 0.25rem;
  box-sizing: border-box;
}

.card__img {
  max-width: 150px;
  margin: 5px;
}

.card__info {
  width: 150px;
  margin: 15px;
}

.card__name {
  font-size: 1.25rem;
  margin: 0;
  margin-bottom: 20px;
}

.card__btn {
  border: none;
  border-radius: 0.25rem;
  background-color: rgba(0, 0, 0, 0.5);
  height: 30px;
  color: #fff;
}
</style>
