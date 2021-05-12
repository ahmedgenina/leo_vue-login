<template>
    <v-form @submit.prevent="$emit(acaoForm, usuario)">
        <label for="nome_de_usuario">Nome de usuário</label>
        <input v-model="usuario.nomeDeUsuario" type="text" title="Nome de usuário" 
        placeholder="Nome de usuário" name="nome_de_usuario">
        
        <label for="senha">Senha</label>
        <input v-model="usuario.senha" type="text" title="Senha" 
        placeholder="Senha" name="senha">


        <button  :title="textoBotao">{{ textoBotao }}</button>
    </v-form>

</template>

<script>
import func from '../../../vue-temp/vue-editor-bridge'

export default {
    name: 'FormUsuario',
    props: ['acaoForm'],
    components: {
    },

    data: function (){
        return {
            usuario: {
                nomeDeUsuario: '',
                senha: ''
            },
        }
    },
    
    computed: {
        textoBotao: function(){
            if (this.acaoForm === 'registrar'){
                return 'Registrar'
            } else {
                return 'Entrar'
            }
        }
    }
}

</script>

<style>

</style>
