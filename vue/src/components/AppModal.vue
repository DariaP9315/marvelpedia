<template>
  <div class="popup" @click="$emit('close-modal')">
    <div class="popup__container" @click.stop>
      <div class="popup__header">
        <h1 class="popup__title">{{ character.name }}</h1>
        <button type="button" class="popup__close" @click="$emit('close-modal')"></button>
      </div>
      <div class="popup__content">
        <img class="popup__img" :src="character.thumbnail" :alt="character.name" />
        <p class="popup__modi">{{ character.modified }}</p>
        <h4 class="popup__description_title">Описание:</h4>
        <p class="popup__description">
          {{ character.description }}
        </p>
        <h4 class="popup__comics_title">Комиксы:</h4>
        <ul class="popup__comics_list">
          <li v-for="(el, idx) in character.comics" :key="idx">
            {{ el.name }}
          </li>
        </ul>
      </div>
      <div class="popup__footer">
        <button type="button" class="popup__footer_btn" @click="$emit('close-modal')">Close</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'AppModal',
  props: ['character'],
};
</script>

<style scoped>
.popup {
  position: fixed;
  height: 100%;
  width: 100%;
  left: 0;
  top: 0;
  overflow-y: scroll;
  padding: 50px 0;
  background-color: #000000da;
}

.popup__container {
  max-width: 600px;
  margin: 1.75rem auto;
  background-color: #fff;
  border: 1px solid rgba(0, 0, 0, 0.25);
  justify-content: center;
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  opacity: 1;
}

.popup__header {
  display: flex;
  justify-content: space-between;
  margin: 0;
  padding: 20px 20px;
  border-bottom: 1px solid rgba(0, 0, 0, 0.5);
}

.popup__close {
  border: none;
  background-color: transparent;
  background-image: url(../../../image/icons-close.svg);
  background-size: cover;
  width: 25px;
  height: 25px;
  align-self: center;
}
.popup__content {
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 0 20px;
  max-width: 570px;
}

.popup__img {
  width: 100%;
  height: auto;
  margin: 30px auto 0;
  object-fit: contain;
}

.popup__modi {
  text-align: start;
  margin-top: 0;
}

.popup__description_title {
  margin: 0;
}
.popup__comics_title {
  margin: 0;
}

.popup__footer {
  border-top: 1px solid rgba(0, 0, 0, 0.5);
  padding: 0 20px;
  display: flex;
  justify-content: end;
}
.popup__footer_btn {
  width: 60px;
  height: 30px;
  border: none;
  background-color: rgb(102, 100, 100);
  color: #fff;
  border-radius: 10px;
  justify-self: end;
  align-self: center;
  margin: 30px 0;
}
</style>
