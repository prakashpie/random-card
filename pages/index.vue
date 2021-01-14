<template>
  <section class="app-section">
    <div class="md-mx-auto md-container--box">
      <div v-if="drawnCardIndex" class="play-card-section">
        <template v-for="index in drawnCardIndex">
          <playing-card :key="index" :card="allCards[index - 1]"></playing-card>
        </template>
      </div>
      <div v-else>
        <div class="md-empty-state">
          <div class="md-empty-state__graphic">
            <div class="md-empty-state__graphic--circle">
              <img alt="banner image" src="/img/clubs.png" class="md-empty-state__img" />
            </div>
          </div>
          <div class="md-empty-state__title">
            Press button to draw random cards
          </div>
          <div class="md-empty-state__subtext">
            Upon clicking, random card will be shown here
          </div>
          <div class="md-empty-state__action--button">
            <button class="md-button md-button--raised md-button--primary" @click="handleDrawCards">
              Draw Cards
            </button>
          </div>
        </div>
      </div>
    </div>
    <div v-if="drawnCardIndex" class="fab-container">
      <button class="md-button md-button--raised md-button--primary" :disabled="drawnCardIndex >= allCards.length" @click="handleDrawCards">
        Draw Cards
      </button>
    </div>
  </section>
</template>

<style lang="scss">
.app-section {
  padding: 24px 0;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}
.md-empty-state__img {
  position: relative;
  max-width: 100%;
  padding: 16px;
}
.md-empty-state__action--button {
  margin-top: 32px;
}
.play-card-section {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 24px;
  @media (max-width: 1200px) {
    grid-template-columns: repeat(3, 1fr);
  }
  @media (max-width: 959px) {
    grid-template-columns: repeat(2, 1fr);
    grid-gap: 16px;
  }
}
.container {
  max-width: 1200px;
  padding: 0 24px;
}
.fab-container {
  position: fixed;
  bottom: 24px;
  right: 24px;
  z-index: 16;
}
.list-enter-active, .list-leave-active {
  transition: all 1s;
}
.list-enter, .list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
</style>

<script>
export default {
  data() {
    return {
      suits: ['hearts', 'spades', 'diamonds', 'clubs'],
      cardValues: ['A', '2', '3', '4', '5', '6', '7', '8', '9', '10', 'J', 'Q', 'K'],
      allCards: [],
      drawnCardIndex: 0
    }
  },
  mounted() {
    this.setAllCards()
  },
  methods: {
    setAllCards() {
      for(let i = 0; i < this.suits.length; i++) {
        for(let j = 0; j < this.cardValues.length; j++) {
          let card = { cardValue: this.cardValues[j], suit: this.suits[i] }
          this.allCards.push(card);
        }
      }
      this.allCards = this.shuffleCard(this.allCards)
    },
    handleDrawCards() {
      if(this.drawnCardIndex >= this.allCards.length) {
        return
      }
      let maxArrIndex = Math.min((this.allCards.length - this.drawnCardIndex), 5);
      this.drawnCardIndex += maxArrIndex
      this.$nextTick(() => {
        const el = document.querySelector(".play-card-section");
        el.scrollIntoView({ behavior: "smooth", block: "end" });
      })
    },
    shuffleCard(list) {
      for (let i = list.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [list[i], list[j]] = [list[j], list[i]];
      }
      return list;
    }
  }
}
</script>
