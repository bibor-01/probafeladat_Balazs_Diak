<template>
    <div class=" p-4">
        <div class="container text-center align-items-center">
            <div class="row row-cols-3 ">
                <div class="col" :class="{ gameElementBord: (index == lastClickIndex), }"
                    v-for="(gameElement, index) in   gameElements  " :key="index" @click="gameElementsBoard(index)"
                    :id="index">
                    <img :src="gameElement.name" :class="{ gameElementOff: (gameElements[index].paired == true) }">
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default ({
    data() {
        return {
            randomGameElement: '',
            lastClickIndex: -1,
        };
    },
    props: {
        gameElements: null,
        releaseSelect: Boolean,
    },
    methods: {
        showGameElements() {
            this.gameElements.forEach(element => {
                console.log(element);
            });


        },
        gameElementsBoard(index) {
            if (this.gameElements[index].paired == false) {
                this.lastClickIndex = index;
                this.$emit('update-selected', index);
            }
        }

    },
    watch: {
        releaseSelect: function (newreleaseSelect, oldreleaseSelect) {
            if (newreleaseSelect == true && oldreleaseSelect == false) {
                if (this.gameElements[this.lastClickIndex].paired == true) {
                    this.lastClickIndex = -1;
                    this.$emit('update-selected', this.lastClickIndex);
                }
            }
        }
    },
    mounted() {
        this.showGameElements();
    }
});
</script>

<style scoped>
.gameElementBord {
    border: 5px dashed #0f0;
}

.gameElementOff {
    filter: grayscale(1);
    background-color: gray;
    margin: 8px;
}
</style>
