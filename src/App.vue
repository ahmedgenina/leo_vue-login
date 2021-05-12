<template>
  <main>
    <section v-if="!usuarioEstaLogado">
      <FormUsuario :acaoForm="acaoForm" @registrar="registrarUsuario" @logar="logarUsuario"></FormUsuario>
      <button type="button" @click="trocaAcaoForm" :title="mensagemTrocaAcaoForm">{{ mensagemTrocaAcaoForm }}</button>
    </section>

    <section v-if="usuarioEstaLogado">
      <p>{{ mensagemUsuarioLogado }} </p>
      <button @click="sair">Sair</button>
    </section>

    <section v-if="mensagemErro">{{ mensagemErro }}</section>
    
    
  </main> 
</template>

<script>

import FormUsuario from './components/FormUsuario/FormUsuario'

export default {
  name: 'App',
  components: {
    FormUsuario
  },

  data: function(){
    return {
      usuariosRegistrados: [],
      usuarioEstaLogado: false,
      nomeUsuarioLogado: '',
      acaoForm: 'registrar',
      mensagemErro: ''
    }
  },

  computed: {
    mensagemTrocaAcaoForm: function(){
      if(this.acaoForm === 'registrar'){
        return 'Já estou registrado'
      } else {
        return 'Registrar-se agora'
      }
    },
    mensagemUsuarioLogado: function(){
      return 'Bem-vindo(a) ' + this.nomeUsuarioLogado + '!'
    }
  },

  methods: {
    registrarUsuario: function(usuario){
      this.mensagemErro = ''

      let buscaUsuario = this.usuariosRegistrados.filter(obj => {
        return obj.nomeDeUsuario === usuario.nomeDeUsuario
      })

      if(buscaUsuario.length === 0){
        this.usuariosRegistrados.push(usuario)
      } else {
        this.mensagemErro = 'Esse usuário já existe'
      }
      
      this.acaoForm = 'logar'
    },
    logarUsuario: function(usuario){
      this.mensagemErro = ''
      let buscaUsuario = this.usuariosRegistrados.filter(obj => {
        return obj.nomeDeUsuario === usuario.nomeDeUsuario
      })

      if (buscaUsuario.length > 0 && usuario.senha === buscaUsuario[0].senha){
        this.nomeUsuarioLogado = usuario.nomeDeUsuario
        this.usuarioEstaLogado = true
      } else {
        this.mensagemErro = 'Este usuário não existe ou a senha está incorreta'
      }
    },
    sair: function(){
      this.mensagemErro = ''
      this.nomeUsuarioLogado = ''
      this.usuarioEstaLogado = false
    },
    trocaAcaoForm: function(){
      this.mensagemErro = ''
      if(this.acaoForm === 'registrar'){
        this.acaoForm = 'logar'
      } else {
        this.acaoForm = 'registrar'
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
