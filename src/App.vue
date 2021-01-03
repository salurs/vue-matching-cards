<template>
    <div class="container position-relative">
<!--        <app-header></app-header>-->
        <h3 class="text-center text-capitalize my-4">Can you match all cards?</h3>
        <app-home></app-home>
        <app-footer></app-footer>
    </div>
</template>

<script>
// import Header from "./components/default/Header";
import Footer from "./components/default/Footer";
import Home from "./components/card/Home";

export default {
    components:{
        // appHeader: Header,
        appFooter: Footer,
        appHome: Home,
    }
}
</script>

<style>

body {
  background: #2b2b2b;
  color: orangered;
  font-family: sans-serif;
}

h3{
    color: lightseagreen;
}
</style>
