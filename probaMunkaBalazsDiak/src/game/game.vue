<template>
  <div class="container px-5 py-5">
    <div class="row justify-content-center row-cols-3 ">
      <div class="col p-2 ">
        <card :id=1 :selectedGameElement=clickToyElement :gameElements=gameElements @paired-success="pairedSuccess">
        </card>
      </div>
      <div class="col p-2">
        <card :id=2 :selectedGameElement=clickToyElement :gameElements=gameElements @paired-success="pairedSuccess">
        </card>
      </div>
      <div class="col p-2">
        <card :id=3 :selectedGameElement=clickToyElement :gameElements=gameElements @paired-success="pairedSuccess">
        </card>
      </div>
    </div>
    <div class="fixed-bottom pool">
      <pool @update-selected="updateSelected" :gameElements=gameElements :releaseSelect=releaseSelect></pool>
    </div>
  </div>
</template>

<script>
import card from "./components/card.vue"
import pool from "./components/pool.vue"
export default ({
  components: {
    card,
    pool
  },
  data() {
    return {
      releaseSelect: false,
      filterElem: false,
      clickToyElement: '',
      gameElements:
        [
          {
            name: '/image/baba1.png',
            category: 'baba',
            paired: false,
          },
          {
            name: '/image/baba2.png',
            category: 'baba',
            paired: false,
          },
          {
            name: '/image/auto1.png',
            category: 'auto',
            paired: false,
          },
          {
            name: '/image/auto2.png',
            category: 'auto',
            paired: false,
          },
          {
            name: '/image/pluss1.png',
            category: 'plüss',
            paired: false,
          },
          {
            name: '/image/pluss2.png',
            category: 'plüss',
            paired: false,
          }
        ]
    }

  },
  methods: {
    updateSelected(payload) {
      this.releaseSelect = false;
      this.clickToyElement = payload;
    },
    pairedSuccess(pairedGameElement) {
      this.gameElements[pairedGameElement].paired = true;
      this.releaseSelect = true;
      let pairedAll = true;
      for (let index = 0; index < this.gameElements.length; index++) {
        if (this.gameElements[index].paired == false) {
          pairedAll = false;
        }
      }
      if (pairedAll) {
        setTimeout(() => {
          alert("nyert")
        }, 500);
      
      }
    }
  },
  mounted() {
    for (let i = this.gameElements.length - 1; i > 0; i--) {
      let j = Math.floor(Math.random() * (i + 1));
      let temp = this.gameElements[i];
      this.gameElements[i] = this.gameElements[j];
      this.gameElements[j] = temp;
    }
  }
})
</script>

<style scoped>
.pool {
  background-image: url('image/pool.png');
  height: 500px;
  padding: 50px;
  background-repeat: no-repeat;
}
</style>