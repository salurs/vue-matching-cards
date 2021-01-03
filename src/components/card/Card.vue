<template>
    <div class="col-md-2 mb-2" :class="{'click-disabled': card.isFlipped, 'matched-opacity': card.isMatched }">
        <div class="box" :style="{height: height}">
            <img v-if="card.isFlipped" :src="'./src/assets/images/'+card.number+'.png'" class="img-fluid h-100" alt="card">
        </div>
    </div>
</template>

<script>
export default {
    name: "Card",
    props: ['card', 'height'],
    data(){
        return{
            clicked: ''
        }
    }
}
</script>

<style scoped>
.box {
    background-color: #1e1e1e;
    display: flex;
    justify-content: center;
    align-self: center;
    align-items: center;
    font-weight: bold;
    max-height: 130px !important;
    cursor: pointer;
    padding: 20px;
}
.click-disabled{
    pointer-events: none;
}
.matched-opacity{
    opacity: .3;
    pointer-events: none;
}

</style>
