<template>
    <div class="screen p-3 row row-cols-2 align-items-center" @click="clickCard" :id="id">
        <div v-for="index in imgElem">
            <div class="col">
                <img :src="gameElements[index].name" class="screenImg">
            </div>
        </div>
    </div>
</template>

<script >


export default ({
    data() {
        return {
            imgElem: [],
            cardCategory: String
        };
    },
    props: {
        id: Number,
        selectedGameElement: Number,
        gameElements: null,
    },
    methods: {
        clickCard() {
            if (this.gameElements[this.selectedGameElement]) {
                if (this.imgElem.length <= 0) {
                    let categoryIsFree = true;
                    for (let index = 0; index < this.gameElements.length; index++) {
                        if (this.gameElements[this.selectedGameElement].category == this.gameElements[index].category) {
                            if (this.gameElements[index].paired) {
                                categoryIsFree = false;
                            }
                        }
                    }
                    if (categoryIsFree == true) {
                        this.cardCategory = this.gameElements[this.selectedGameElement].category
                        this.imgElem.push(this.selectedGameElement)
                        this.$emit('paired-success', this.selectedGameElement);
                    }

                } else if (this.gameElements[this.selectedGameElement].category == this.cardCategory) {
                    this.imgElem.push(this.selectedGameElement)
                    this.$emit('paired-success', this.selectedGameElement);
                };


            }

        },

    },


})
</script>

<style scoped>
.screen {
    background-image: url('image/screen.png');
    height: 300px;
    background-repeat: no-repeat;
    background-size: contain;
}

.screenImg {
    width: 160px;
}
</style>
