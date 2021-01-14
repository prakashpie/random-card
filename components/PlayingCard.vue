<template>
  <div class="md-card playing-card md-card--outlined">
    <div class="playing-card__top-corner">
      <div class="playing-card__corner-text">{{ card.cardValue }}</div>
      <img :src="`/img/${card.suit}.png`" class="playing-card__corner-img" />
    </div>
    <div class="playing-card__bottom-corner">
      <div class="playing-card__corner-text">{{ card.cardValue }}</div>
      <img :src="`/img/${card.suit}.png`" class="playing-card__corner-img" />
    </div>
    <div class="playing-card__name">{{card.cardValue}}</div>
  </div>
</template>

<style lang="scss">
.playing-card {
  position: relative;
  width: 250px;
  min-width: 0;
  height: 350px;
  padding: 32px;

  @media (max-width: 959px) {
    max-width: 250px;
    width: calc(50vw - 32px);
  }

  @media (max-width: 767px) {
    height: auto;
    padding-bottom: 127%;
  }

  &__corner-text {
    font-weight: 700;
    margin-bottom: 2px;
  }

  &__corner-img {
    max-width: 24px;
  }

  &__top-corner {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    position: absolute;
    top: 8px;
    left: 4px;
    width: 24px;
  }
  &__bottom-corner {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    position: absolute;
    bottom: 8px;
    right: 4px;
    width: 24px;
    transform: rotate(180deg);
  }
  &__name {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    font-size: 56px;
    font-weight: 700;
    @media (max-width: 767px) {
      font-size: 40px;
    }
  }
}
</style>

<script>
export default {
  props: {
    card: {
      type: Object
    }
  }
}
</script>
