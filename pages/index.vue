<template>
  <div>
    <div class="mt-4">
      <v-dialog
        v-model="dialog"
        tile
        width="300"
      >
        <template v-slot:activator="{ on, attrs }">
          <v-btn
            v-bind="attrs"
            v-on="on"
          >
            入力
          </v-btn>
        </template>

        <v-card>
          <v-card-title>
            数値の入力
          </v-card-title>

          <v-card-text>
            <v-text-field
              v-model="inputNumber"
            ></v-text-field>
          </v-card-text>

          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn
              text
              @click="add(inputNumber)"
            >
              入力
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </div>

    <div class="mt-10">
      <v-row justify="center" align="center" max-height="500">
        <v-col cols="3" v-for="index in boxNumber" :key="index">
          <v-card>
            <v-card-text>{{ index }}</v-card-text>
            <v-card-title
              v-if="typeof numbers[index - 1] !== 'undefined'"
            >
              {{ numbers[index - 1] }}
            </v-card-title>
          </v-card>
        </v-col>
      </v-row>
    </div>
  </div>
</template>

<script>
const boxNumber = 100
export default {
  data() {
    return {
      dialog: false,
      inputNumber: 0,
      boxNumber,
      numbers: [],
    }
  },
  methods: {
    add(value) {
      // メソッド名と処理の不一致感
      // 要リファクタ

      this.numbers.push(value)

      this.dialog = false
      this.inputNumber = 0
    },
  },
  mounted() {
  },
}
</script>

