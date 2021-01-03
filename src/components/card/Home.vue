<template>
    <div class="row">
        <div class="col-md-12">
            <app-card-nav v-if="isHome" @click.native="start(0)" :index="0"></app-card-nav>
            <app-card-nav v-if="isHome" @click.native="start(1)" :index="1"></app-card-nav>
            <app-card-nav v-if="isHome" @click.native="start(2)" :index="2"></app-card-nav>
            <app-card-nav v-if="isHome" @click.native="start(3)" :index="3"></app-card-nav>
            <app-card-nav v-if="isHome" @click.native="start(4)" :index="4"></app-card-nav>
            <app-card-nav v-if="isHome" @click.native="start(5)" :index="5"></app-card-nav>
            <app-detail v-else :cards="cards"></app-detail>
        </div>
    </div>
</template>

<script>
import _ from 'lodash';
import CardNav from "./CardNav";
import Detail from "./Detail";

export default {
    name: "Home",
    components: {
        appCardNav: CardNav,
        appDetail: Detail,
    },
    data() {
        return {
            isHome: true,
            data: [],
            cards: [],
        }
    },
    methods: {
        start(index) {
            this.isHome = false;
            let count = (index * 6 + 12) / 2;
            for (let i = 1; i <= count; i++) {
                let number = Math.floor(Math.random() * 50) + 1;
                let card = {number, isFlipped: false, isMatched: false}
                let found = this.data.some(el => el.number === card.number);//check for unique number
                if (!found) {
                    this.data.push(card);
                }else{
                    i--;
                }
            }
            let cards1 = _.cloneDeep(this.data);
            let cards2 = _.cloneDeep(this.data);
            this.cards = this.cards.concat(cards1, cards2);
        },
    }
}
</script>

<style scoped>

</style>
