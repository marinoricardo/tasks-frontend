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
            <v-text-field label="Nome da tarefa"></v-text-field>
          </v-col>
          <v-col cols="6">
            <v-text-field label="Descrição"></v-text-field>
          </v-col>
          <v-col cols="3">
            <v-btn block color="#F25675" dark>Adicionar</v-btn>
          </v-col>
        </v-row>

        <br />
        <br />
        <v-list flat subheader three-line>
          <v-subheader>Minhas Tarefas</v-subheader>
          <v-list-item-group v-model="settings" multiple active-class>
            <v-list-item>
              <template v-slot:default="{ active }">
                <v-list-item-action>
                  <v-checkbox :input-value="active" color="#F25675"></v-checkbox>
                </v-list-item-action>

                <v-list-item-content>
                  <v-list-item-title>Notifications</v-list-item-title>
                  <v-list-item-subtitle>Notify me about updates to apps or games that I downloaded</v-list-item-subtitle>
                </v-list-item-content>
              </template>
            </v-list-item>

            <v-list-item>
              <template v-slot:default="{ active }">
                <v-list-item-action>
                  <v-checkbox :input-value="active"></v-checkbox>
                </v-list-item-action>

                <v-list-item-content>
                  <v-list-item-title>Sound</v-list-item-title>
                  <v-list-item-subtitle>Auto-update apps at any time. Data charges may apply</v-list-item-subtitle>
                </v-list-item-content>
              </template>
            </v-list-item>

            <v-list-item>
              <template v-slot:default="{ active }">
                <v-list-item-action>
                  <v-checkbox :input-value="active"></v-checkbox>
                </v-list-item-action>

                <v-list-item-content>
                  <v-list-item-title>Auto-add widgets</v-list-item-title>
                  <v-list-item-subtitle>Automatically add home screen widgets when downloads complete</v-list-item-subtitle>
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
  width: 400px;
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

export default {
  name: 'App',

  data: () => ({
    //
  }),
};
</script>
