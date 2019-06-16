<template>
<div>
    <h1 class="with-border">Ahorra con energia 100% verde</h1>
    <div>
        <nuxt-link class="btn-tarifa" to="/create">Ver tarifas</nuxt-link>
    </div>
</div>
</template>

<style scoped>

.with-border {
    border-image:linear-gradient(to right, #e6007d, #ffdc00) 1;
    border-bottom:2px solid;
    padding:2rem;
    margin-bottom:2rem;
}
.btn-tarifa {
    margin-top:20px;
    font-size:1.125rem;
    background-color: #e6007d;
    padding:1rem 1.5rem;
    color:#fff;
    margin:2rem;
}
</style>
