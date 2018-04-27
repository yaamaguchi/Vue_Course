<template>
    <div>
        <slot name="cabecalho" class="header" ></slot>
        <hr>
        <slot class="body"></slot>
        <hr>
        <slot name="rodape" class="footer"></slot>
    </div>


    <!-- <componente-qualquer>
        <div slot="cabecalho">
            <h1>Bem-vindo!</h1>
        </div>
        <p>Seja bem-vindo à Alura!</p>
        <div slot="rodape">
            <p>copyright 2017</p>
        </div>
    </componente-qualquer> -->

</template>

<script>
export default {
}

</script>

<style scoped>

</style>
