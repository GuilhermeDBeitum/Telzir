<template>
  <router-link style="color: black; text-decoration: none" to="Simulador">
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

      <v-row align="center" justify="center">
        <v-img class="ctr" src="../assets/hand.png"></v-img>
      </v-row>

      <br />
    </v-container>
  </router-link>
</template>

<script>
export default {
  name: "Intro",
  components: {},
};
</script>
<style scoped>
.init {
  margin: 30%;
}
.ctr {
  position: absolute;
  margin-left: 80px;
  bottom: 0;
  width: 60vh;
  margin-top: 10px;
}
</style>
