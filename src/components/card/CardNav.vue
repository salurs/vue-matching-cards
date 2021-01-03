<template>
    <div class="card shadow-lg mb-4">
        <div class="d-flex align-items-center justify-content-between">
            <div>
                <span class="fw-bold d-inline-block number">#{{ index + 1 }}</span>
                <span class="fw-bold d-inline-block mx-3 number-card">{{ index * 6 + 12 }} Cards</span>
            </div>
            <a class="btn btn-outline-danger btn-sm d-inline-block float-end"><img :src="'./src/assets/icons/play.png'" style="width: 25px;" alt="play"></a>
        </div>
    </div>
</template>

<script>
export default {
    props: ['index']
}
</script>

<style scoped>
.card {
    border-radius: 0;
    padding: 15px;
    background: #333;
    border-color: orangered;
    cursor: pointer;
}

.number-card {
    font-size: 20px;
}
.btn-outline-danger{
    border: none;
}
.btn-outline-danger:hover{
    background-color: lightseagreen !important;
}
</style>
