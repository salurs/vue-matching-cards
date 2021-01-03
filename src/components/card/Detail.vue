<template>
    <div class="row">
        <app-card
            @click.native="selectedCard($event,card)"
            v-for="card in cards"
            :style="{'pointer-events': selectedCards.length == 2 || card.isMatched ? 'none' : ''}"
            :card="card"
            :selectedCards="selectedCards"
            :height="420 * 7 / cards.length + 'px'"></app-card>

        <div class="col-md-12">
            <div class="info-area shadow-lg mb-5">
                <div class="row">
                    <div class="col-md-3 d-flex justify-content-center flex-column align-items-center">
                        <span class="d-inline-block number-area">{{ time }}</span>
                        <span class="d-inline-block">Timer</span>
                    </div>
                    <div class="col-md-3 d-flex justify-content-center flex-column align-items-center">
                        <span class="d-inline-block number-area">{{ score }}</span>
                        <span class="d-inline-block">Score</span>
                    </div>
                    <div class="col-md-3 d-flex justify-content-center flex-column align-items-center">
                        <span class="d-inline-block number-area">{{ moves }}</span>
                        <span class="d-inline-block">Moves</span>
                    </div>
                    <div class="col-md-3 text-center">
                        <button type="button" class="btn btn-outline-danger" @click="giveup">Give up</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Card from "./Card";

export default {
    name: "Detail",
    props: ['cards', 'isHome'],
    components: {
        appCard: Card,
    },
    data() {
        return {
            selectedCards: [],
            timer: null,
            moves: 0,
            score: 0,
            time: 0,
            isFinish: true,
        }
    },
    created() {
        this.shuffle(this.cards);
        this.timer = setInterval(() => {
            this.time++;
        }, 1000);
    },
    methods: {
        shuffle(array) {
            array.sort(() => Math.random() - 0.5);
        },
        selectedCard(event,card) {
            let found = this.selectedCards.some(el => el === card);
            if (!found) {
                card.isFlipped = true;
                this.selectedCards.push(card);
                if (this.selectedCards.length == 2) {
                    if (this.selectedCards[0].number == this.selectedCards[1].number) {
                        this.selectedCards.forEach(card => card.isMatched = true);
                        this.selectedCards = [];
                        this.score += 25 - Math.round(this.time / 10 + this.moves/5);
                        if (this.score <= 0) this.score = 0;
                        if (this.cards.every(el => el.isMatched === true)) {
                            this.moves++;
                            this.isFinish = true;
                            clearInterval(this.timer);
                            this.score += 50;
                            // this.playAgain();
                            this.runSweetAlert();
                        }
                    } else {
                        setTimeout(() => {
                            this.selectedCards.forEach(el => el.isFlipped = false);
                            this.selectedCards = [];
                        }, 1000)
                    }
                    this.moves++;
                }
            }
        },
        giveup() {
            window.location.replace('/');
        },
        playAgain(){
            this.cards.forEach(el=>{
                el.isMatched = false;
                el.isFlipped = false;
            });
            this.time = 0;
            this.moves = 0;
            this.score = 0;
            this.timer = setInterval(() => {
                this.time++;
            }, 1000);
        },
        runSweetAlert(){
            this.$swal.fire({
                title: 'Congratulations!',
                html: `<div class="py-3 d-flex justify-content-evenly"><span><b>Score: </b>${this.score}</span>  <span><b>Moves: </b>${this.moves}</span>  <span><b>Time: </b>${this.time} s</span></div>`,
                icon: 'success',
                showCancelButton: true,
                confirmButtonColor: '#333',
                cancelButtonColor: 'lightseagreen',
                cancelButtonText: 'Try Again',
                confirmButtonText: 'Go Home'
            }).then((result) => {
                if (result.isConfirmed) {
                    window.location.replace('/');
                }else{
                    this.playAgain();
                }
            });
        }
    }

}

</script>

<style scoped>

.info-area {
    padding: 15px;
    background-color: #222;
}

.info-area span {
    color: #dc3545;
}

.number-area {
    padding: 5px 0;
    width: 100px;
    text-align: center;
    border-radius: 5px;
    border: 1px solid #dc3545;
}

</style>
