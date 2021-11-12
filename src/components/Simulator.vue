<template>
  <v-layout>
    <v-container class="my-4">
      <v-row>
        <v-card class="elevation-16">
          <v-col cols="12" md="12" class="my-8">
            <h4 tile class="text-center my-1">SIMULADOR</h4>

            <v-card light outlined tile>
              <v-row>
                <v-col>
                  <v-col
                    cols="12"
                    class="text-center black--text font-weight-black"
                  >
                    <p class="black--text font-weight-black">ORIGEM</p>
                    <v-select
                      class="barjust elevation-5"
                      color="blue"
                      autocomplete="off"
                      type="number"
                      :items="sourceDdd"
                      @click="changeInput"
                      label="DDD"
                      v-model="source"
                      outlined
                    ></v-select>
                  </v-col>
                </v-col>

                <v-col>
                  <v-col
                    cols="12"
                    class="text-center black--text font-weight-black"
                  >
                    <p class="black--text font-weight-black">DESTINO</p>
                    <v-select
                      class="barjust elevation-5"
                      color="blue"
                      autocomplete="off"
                      type="number"
                      :items="destinyDdd"
                      @click="changeInput"
                      label="DDD"
                      v-model="destiny"
                      outlined
                    ></v-select>
                  </v-col>
                </v-col>

                <v-col>
                  <v-col
                    cols="12"
                    class="text-center black--text font-weight-black"
                  >
                    <p class="black--text font-weight-black">TEMPO</p>

                    <input
                      class="barjust time elevation-5"
                      autocomplete="off"
                      color="blue"
                      v-model="time"
                      placeholder="MIN"
                      type="number"
                      @input="assertMaxChars()"
                    />
                  </v-col>
                </v-col>

                <v-col>
                  <v-col
                    cols="12"
                    class="text-center black--text font-weight-black"
                  >
                    <p class="black--text font-weight-black">PLANO</p>
                    <v-select
                      class="barjust plan elevation-5"
                      color="blue"
                      autocomplete="off"
                      type="number"
                      :items="plansFale"
                      label="FALEMAIS"
                      v-model="plan"
                      outlined
                    ></v-select>
                  </v-col>
                </v-col>

                <v-col>
                  <v-col
                    class="
                      text-center
                      black--text
                      font-weight-black
                      my-5
                      elevation-5
                    "
                  >
                    <p class="black--text font-weight-black">SEM FALEMAIS</p>
                    <v-data class="barjust">{{
                      formatCash(this.calculateWithoutFalemais())
                    }}</v-data>
                  </v-col>
                </v-col>

                <v-col>
                  <v-col
                    class="
                      text-center
                      black--text
                      font-weight-black
                      green--text
                      fontsize
                      my-5
                      elevation-18
                    "
                  >
                    <p class="black--text font-weight-black">COM FALEMAIS</p>
                    <v-data class="barjust">{{
                      formatCash(this.calculateWithFalemais())
                    }}</v-data>
                  </v-col>
                </v-col>
              </v-row>

              <h6 class="adjust text-center black--text font-weight-black">
                após a carência do plano contratado taxa de 10%/min.
              </h6>
            </v-card>

            <hr />
          </v-col>
        </v-card>
      </v-row>

      <!-- Se quiser um botao para limpar todos os inputs -->

      <!-- <v-row align="center" justify="center">
        <v-btn
          fixed
          dark
          bottom
          @click="resetVars()"
          class="text-center my-7 elevation-18"
          color="black"
          max-width="190"
        >
          <v-icon>Novo Cálculo</v-icon>
        </v-btn>
      </v-row>-->
    </v-container>
  </v-layout>
</template>

<script>
export default {
  components: {},

  data() {
    return {
      maxLengthInCars: 5,
      text: "",
      source: 0,
      destiny: 0,
      time: null,
      plan: 0,
      cost: 0,
      withFalemais: 0,
      withoutFalemais: 0,
      sourceDdd: ["011", "016", "017", "018"],
      destinyDdd: ["011", "016", "017", "018"],
      plansFale: ["Fale+30", "Fale+60", "Fale+90", "Fale+120"],
    };
  },
  computed: {},

  methods: {
    calculateWithoutFalemais() {
      let sourceC = this.source;
      let destinyC = this.destiny;
      let vtime = this.time;

      let vTotal = 0;
      let tariff = 0;
      this.tariff = tariff;

      if (vtime < 0) {
        vtime = null;
      }

      if (sourceC === "011" && destinyC === "016") {
        this.tariff = 1.9;
        vTotal = 1.9 * vtime;
      } else if (sourceC === "016" && destinyC === "011") {
        this.tariff = 2.9;
        vTotal = 2.9 * vtime;
      } else if (sourceC === "011" && destinyC === "017") {
        this.tariff = 1.7;
        vTotal = 1.7 * vtime;
      } else if (sourceC === "017" && destinyC === "011") {
        this.tariff = 2.7;
        vTotal = 2.7 * vtime;
      } else if (sourceC === "011" && destinyC === "018") {
        this.tariff = 0.9;
        vTotal = 0.9 * vtime;
      } else if (sourceC === "018" && destinyC === "011") {
        this.tariff = 1.9;
        vTotal = 1.9 * vtime;
      }

      return vTotal;
    },

    calculateWithFalemais() {
      let maisplan = this.plan;
      let vtime = this.time;
      let vtariff = this.tariff;

      let vTotal = 0;
      this.vTotal = vTotal;

      switch (maisplan) {
        case "Fale+30":
          if (vtime <= 30) {
            return (this.vTotal = 0);
          } else {
            return (this.vTotal =
              (vtariff + vtariff * (10 / 100)) * (vtime - 30));
          }

        case "Fale+60":
          if (vtime <= 60) {
            return (this.vTotal = 0);
          } else {
            return (this.vTotal =
              (vtariff + vtariff * (10 / 100)) * (vtime - 60));
          }

        case "Fale+90":
          if (vtime <= 90) {
            return (this.vTotal = 0);
          } else {
            return (this.vTotal =
              (vtariff + vtariff * (10 / 100)) * (vtime - 90));
          }

        case "Fale+120":
          if (vtime <= 120) {
            return (this.vTotal = 0);
          } else {
            return (this.vTotal =
              (vtariff + vtariff * (10 / 100)) * (vtime - 120));
          }

        default:
          return (this.vTotal = 0);
      }
    },

    formatCash(n) {
      return (
        "$ " +
        n
          .toFixed(2)
          .replace(".", ",")
          .replace(/(\d)(?=(\d{3})+,)/g, "$1.")
      );
    },

    changeInput() {
      let sourceC = this.source;
      let destinyC = this.destiny;

      switch (sourceC) {
        case "":
          this.destinyDdd = ["", "011", "016", "017", "018"];
          break;
        case "011":
          this.destinyDdd = ["011", "016", "017", "018"];
          break;

        case "016":
          this.destinyDdd = ["011"];
          break;

        case "017":
          this.destinyDdd = ["011"];
          break;

        case "018":
          this.destinyDdd = ["011"];
          break;
        default:
          break;
      }

      switch (destinyC) {
        case "":
          this.sourceDdd = ["", "011", "016", "017", "018"];
          break;
        case "011":
          this.sourceDdd = ["011", "016", "017", "018"];
          break;

        case "016":
          this.sourceDdd = ["011"];
          break;

        case "017":
          this.sourceDdd = ["011"];
          break;

        case "018":
          this.sourceDdd = ["011"];
          break;
        default:
          break;
      }
    },

    // Se quiser um botao para limpar todos os inputs
    resetVars() {
      this.source = 0;
      this.destiny = 0;
      this.time = null;
      this.plan = 0;
    },
    assertMaxChars: function () {
      if (this.time.length >= this.maxLengthInCars) {
        this.time = this.time.substring(0, this.maxLengthInCars);
      }
      if (this.time == this.pattern) {
        this.time = null;
      }
      if (this.time == -1) {
        this.time = null;
      }
    },
  },

  mounted() {},
};
</script>

<style lang="scss">
.adjust {
  margin-bottom: 10px;
}

.barjust {
  height: 55px;
}

.plan {
  width: 150px;
}

.time {
  outline-color: rgb(38, 131, 207);
  border-color: black;
  border: 1px solid #706e6e;
  border-radius: 5%;
  padding: 14px;
  resize: none;
  height: 55px;
  width: 100px;
}
</style>
