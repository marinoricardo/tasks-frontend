<template>
  <v-app>
    <v-main class="app">
      <v-container class="container">
        <h1>Tarefas</h1>
        <hr />
        <br />
        <br />
        <v-row>
          <v-col cols="3">
            <v-text-field label="Nome"></v-text-field>
          </v-col>
          <v-col cols="9">
            <v-text-field label="Descrição"></v-text-field>
          </v-col>
          <v-row>
            <v-col cols="12">
              <v-btn block color="#F25675" dark>Adicionar</v-btn>
            </v-col>
          </v-row>
        </v-row>

        <br />
        <br />
        <v-list flat subheader three-line>
          <v-subheader>Minhas Tarefas</v-subheader>
          <v-list-item-group v-model="settings" multiple active-class v-for="item in tasks.data" :key="item.id">
            <v-list-item>
              <template v-slot:default="{ active }">
                <v-list-item-action>
                  <v-checkbox :input-value="active" color="#F25675"></v-checkbox>
                </v-list-item-action>

                <v-list-item-content>
                  <v-list-item-title>{{ item.nome}}</v-list-item-title>
                  <v-list-item-subtitle>{{ item.descricao }}</v-list-item-subtitle>
                </v-list-item-content>
              </template>
            </v-list-item>
          </v-list-item-group>
        </v-list>
      </v-container>
    </v-main>
  </v-app>
</template>

<style>
.app {
  background-color: #fefefe;
  background-image: linear-gradient(#fc6c48 0%, #ef5081 100%);
}
.container {
  width: 500px;
  /* max-width: 100%; */
  min-height: 500px;
  margin: 20px auto 40px;
  border: 1px solid #eee;
  border-radius: 4px;
  padding: 40px 20px;
  -webkit-box-shadow: 0 0 15px 0 rgba(0, 0, 0, 0.05);
  box-shadow: 0 0 15px 0 rgba(0, 0, 0, 0.05);
  background-color: #f4f7fc;
  overflow: hidden;
  position: relative;
}
</style>

<script>
import axios from 'axios'

export default {
  name: 'App',
  data() {
    return {
      tasks: [],
      settings: []
    }
  },
  created(){
    this.getTasks()
  },
  methods:{
    getTasks(){
      axios.get('http://tasks.test/api/tarefas').then((data) =>{
        this.tasks = data.data
        console.log(data)
      })
    }
  }
};
</script>
