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
            <v-text-field v-model="task.nome" label="Nome"></v-text-field>
          </v-col>
          <v-col cols="9">
            <v-text-field v-model="task.descricao" label="Descrição"></v-text-field>
          </v-col>
          <v-row>
            <v-col cols="12">
              <v-btn block color="#F25675" dark @click="addTask()">Adicionar</v-btn>
            </v-col>
            <v-col cols="12">
              <div class="text-center">
                <v-progress-circular
                  class="teste"
                  v-show="spinner"
                  :size="70"
                  :width="7"
                  color="purple"
                  indeterminate
                ></v-progress-circular>
              </div>
              <v-snackbar v-model="snackbar" :timeout="timeout">
                {{ text }}
                <template v-slot:action="{ attrs }">
                  <v-btn color="blue" text v-bind="attrs" @click="snackbar = false">Fechar</v-btn>
                </template>
              </v-snackbar>
            </v-col>
          </v-row>
        </v-row>

        <br />
        <br />

        <v-simple-table>
          <template v-slot:default>
            <thead>
              <tr>
                <th class="text-left">Nome</th>
                <th class="text-left">Descrição</th>
                <th class="text-left">Feito</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="item in tasks.data" :key="item.id">
                <td>{{ item.nome }}</td>
                <td>{{ item.descricao }}</td>
                <td>
                  <v-checkbox @change="done" color="red" :value="item.id" hide-details></v-checkbox>
                </td>
              </tr>
            </tbody>
          </template>
        </v-simple-table>
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
      snackbar: false,
      text: 'Tarefa adicionada com sucesso.',
      timeout: 2000,
      spinner: false,
      task: {
        nome: "",
        descricao: ""
      },
      tasks: [],
      settings: [],
      desserts: [
        {
          name: 'Frozen Yogurt',
          calories: 159,
        },
        {
          name: 'Ice cream sandwich',
          calories: 237,
        },
      ]
    }
  },
  created() {
    // this.spinner = false
    this.getTasks()
  },
  methods: {
    getTasks() {
      this.spinner = true
      axios.get('http://tasks.test/api/tarefas').then((data) => {
        this.tasks = data.data
        this.spinner = false
        console.log(data)
      })
    },
    addTask() {
      this.spinner = true
      axios.post('http://tasks.test/api/tarefas', this.task).then((data) => {
        console.log(data)
        this.snackbar = true
        this.spinner = false
        this.getTasks()
        this.task.nome = ""
        this.task.descricao = ""
      })
    },
    done(e) {
      axios.delete(`http://tasks.test/api/tarefas/${e}`).finally(() => {
        this.getTasks()
      })

    }
  },

};
</script>
