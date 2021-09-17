<template>
  <v-container>
    <br />
    <br />
    <v-row md="5" cols="12">
      <v-card color="blue">
        <v-col md="12" cols="12">
          <span class="white--text font-weight-black">
            Você pode simular uma ligação com um de nossos planos.
          </span>

          <p class="white--text font-weight-black">
            Comprove as vantagens de fazer parte do FaleMais!
          </p>
        </v-col>
      </v-card>
    </v-row>
    <router-link style="color:black; text-decoration:none;" to="Simulador">
      <v-row align="center" justify="center">
        <h1 class="white--text font-weight-black ">COMEÇAR</h1>
        <v-img class="ctr" max-width="360" src="..\assets\hand.png"></v-img>
      </v-row>
    </router-link>
    <br />
  </v-container>
</template>

<script>
export default {
  name: "Intro",
  components: {},
};
</script>
<style scoped>
.ctr {
  margin-left: 75px;
}
</style>
