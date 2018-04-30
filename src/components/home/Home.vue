<template>
    <div>
        <h1 class="centralizado">{{ titulo }}</h1>
        
        <input type="search" class="filtro" @input="filtro = $event.target.value" placeholder="filtre pelo titulo">
       
        <ul class="lista-fotos">
            <li class="lista-fotos-item" v-for="pic in fotosComFiltro">
                <meu-painel :titulo="pic.titulo">
                    <imagem-responsiva v-meu-transform :url="pic.url" :titulo="pic.titulo"/>
                    <meu-botao tipo="button" rotulo="Remover" estilo="perigo" :confirmacao="false" @botaoAtivado="remove($event, pic)"/>
                </meu-painel>
            </li>
        </ul>

        <!--<h1 v-text="titulo"></h1>
        ul>li*2>img 
        div.painel>h2.painel-titulo+div.painel-conteudo -->
        <!-- <div class="painel"><h2 class="painel-titulo">{{pic.titulo}}</h2><div class="painel-conteudo"><img class="imagem-responsiva" :src="pic.url" :alt="pic.titulo"></div></div> -->
        <!-- <img v-bind:src="foto.url" v-bind:alt="foto.titulo"> <img :src="foto1.url" :alt="foto1.titulo"> -->
    </div>
</template>

<script>
    import Painel from '../shared/painel/Painel.vue';
    import ImagemResponsiva from '../shared/imagem-responsiva/ImagemResponsiva.vue';
    import Botao from '../shared/botao/Botao.vue';

    export default {
        components:{
            'meu-painel' : Painel, 
            'imagem-responsiva' : ImagemResponsiva,
            'meu-botao' : Botao
        },
        computed:{
            fotosComFiltro(){
                if(this.filtro){
                    let exp = new RegExp(this.filtro.trim(), 'i');

                    return this.fotos.filter(foto => exp.test(foto.titulo));
                }else{
                    return this.fotos;
                }
            }
        },
        methods:{
            remove($event, foto){
                //alert($event);
                alert('Remover a foto:=> ' + foto.titulo);
            }
        },
        data(){
            return{
                titulo : 'Alurapic',
                fotos :[],
                filtro: ''

                /*fotos : [ {url : '', titulo: ''}]*/
            }
        },
        created(){
            this.$http.get('http://localhost:3000/v1/fotos')
                .then( res => res.json())
                .then( fotos => this.fotos = fotos, err => console.log('Erro'));
        }
    }

</script>

<style >
    .centralizado{text-align: center;}

    .lista-fotos{list-style: none;}

    .lista-fotos-item{display: inline-block;}

    .filtro{display: block;width: 100%;}
</style>
