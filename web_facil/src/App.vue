<template>
  <div id="app">
    <div class="shadow bg-white" id="container">
      <h2 id="text_header">Sobre o profissional</h2>
      <h3 id="text_sub_header">Dados do profissional</h3>
      <div id="container_form_img">
        <form class="form">
          <div id="name" class="form-group">
            <label class="label" for="name">Nome completo*</label>
            <input v-model="name" class="form-control"  placeholder="Digite o nome completo">
            <span v-if="msg.name">{{msg.name}}</span>
          </div>
          <div class="form-group mb-4 mt-4">
            <label class="label" for="exampleInputPassword1">CPF*</label>
            <input v-mask="'###.###.###-##'" class="form-control wd-8" id="small_input" v-model="cpf" placeholder="Digite um CPF">
          </div>
          <div class="form-group mb-4 mt-4">
            <label class="label" for="exampleInputPassword1">Número de celular*</label>
            <input v-mask="'(##) # ####-####'" v-model="phone" class="form-control wd-8" id="small_input" placeholder="(00) 0 0000-0000">
          </div>
          <div class="container_selector">
            <div class="container_label_select">
              <label class="label">Estado*</label>
              <select v-model="state" @change="setState()" id="small_selector" class="form-select">
                <option value="" selected disabled hidden>Selecione</option>
                <option value="1">Paraná</option>
                <option value="2">Rio grande do Sul</option>
                <option value="3">Santa catarina</option>
              </select>
            </div>
            
            <div class="container_label_select">
              <label class="label">Cidade*</label>
              <select id="small_selector" class="form-select" aria-label="Default select example">
                <option value="" selected disabled hidden>Selecione</option>
                <option v-for="city in cities_selected" :value="city.name" :key="city.value">{{city}}</option>
              </select>
            </div>
          </div>
          
        </form>
        <img id="img" src="@/assets/desktop_pagina_1.png"/>
      </div>
      <div class="container_label_progress">
        <div class="container_progress">
          <div id="progress"/>
        </div>
        <label id="label_progress">1 de 2</label>
      </div>
      <Button msg="PRÓXIMO"/>
    </div>
  </div>
</template>

<script>

import Button from './components/button.vue'

export default {
  
  name: 'App',
  components: {
    Button
  },
  data(){
    return{
      name: '',
      name_valid: false,
      msg: [],
      cpf: '',
      phone: '',
      error_color: "#ff0000",
      state: '',
      cities_selected: [],
      cities: [
        {
          value: 1,
          names: ['Londrinha','Maringá']
        },
        {
          value: 2,
          names: ['Pelotas','Porto Alegre']
        },
        {
          value: 3,
          names: ['Florianópolis','Joinville']
        },
      ]
    }
  },
  watch:{
    name(value){
      this.name = value;
      this.validateName(value)
    }
  },
  methods:{
    validateName(value){
      if (value.length > 3 && value.length < 47){
        this.msg['name'] = '';
        this.name_valid = true;
      } else{
        this.msg['name'] = 'Nome inválido';
        this.name_valid = false;
      }
    },
    setState(){
      this.cities.map((item) => {
        if(item.value == this.state){
          this.cities_selected = item.names
        }
      })
    }
  }
}
</script>

<style>

#app {
  background: #FFE766;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center; 
  color: #000;
}
#container{
  background: #fff;
  height: auto;
  width: 60%;
  padding: 50px 0px 50px 50px;
  border-radius: 20px;
  
}
.container_label_select{
  display: flex;
  flex-direction: column;
  width: 100%;
}
.container_selector{
  display: flex;
  flex-direction: row;
}
.container_label_progress{
  display: flex;
  flex-direction: row;
  align-items: center;
  margin-top: 16px;
}
.label{
  font-family: 'Comfortaa', cursive;
  margin-bottom: 4px;
  font-size: 12px;
}
.container_progress{
  width: 30%;
  height: 25px;
  background: #dcdcdc;
  border-radius: 4px;
}
#progress{
  width: 50%;
  height: 100%;
  background: #483698;
  border-radius: 4px;
}
#label_progress{
  margin-left: 16px;
  color: #483698;
  font-family: 'Open Sans', sans-serif;
}
#text_header{
  font-family: 'Comfortaa', cursive;
  font-size: 42px;
  font-weight: 500;
  color: #483689
}
#text_sub_header{
  color: #000;
  font-family: 'Comfortaa', cursive;
  font-weight: 700;
  font-size: 22px;
  margin-top: 32px;
  margin-bottom: 32px;
}
#container_form_img{
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  height: auto;
}
#img{
  width: 50%;
}
.form{
  width: 100%
}
#name{
  width: 90%
}
#small_input{
  width: 70%
}
#small_selector{
  width: 80%;
  margin-right: 15px
}

@media screen and (max-width: 829px) {
    #container{
      width: 100%;
      margin-top: 350px;
      border-bottom-left-radius: 0px;
      border-bottom-right-radius: 0px;
      border-top-left-radius: 50px;
      border-top-right-radius: 50px;
      padding: 50px 0px 50px 20px;
    }
    #img{
      display: none;
    }
    .container_progress{
      width: 70%;
    }
    #text_header{
      font-size: 24px;
    }
    #text_sub_header{
      font-size: 18px;
    }
}

</style>
