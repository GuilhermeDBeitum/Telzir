<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <v-row class="text-center my-7 elevation-18">
        <v-col md="1" cols="3">
          <router-link style="color:white; text-decoration:none;" to="/">
            <span class="title ml-3 mr-5">FaleMais</span>
          </router-link>
        </v-col>
        <v-col md="1" cols="7">
          <router-link style="color:white; text-decoration:none;" to="/">
            <v-img width="33" src=".\assets\cellphone.jpg"></v-img>
          </router-link>
        </v-col>
      </v-row>
    </v-app-bar>

    <v-img height="600" src=".\assets\background.png">
      <v-col cols="13" md="6" class="mx-auto black--text"></v-col>

      <router-view></router-view>
    </v-img>
    <v-footer app height="30" color="primary">
      <span style="color:white;"
        >&copy; FaleMais 2020. Todos os direitos reservados.</span
      >
    </v-footer>
  </v-app>
</template>

<script>
export default {
  name: "App",

  components: {},

  data: () => ({
    //
  }),
};
</script>
