<template>
  <div>
    <div class="mt-4">
      <v-dialog
        v-model="addDialog"
        tile
        width="200"
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
            <v-form ref="form">
              <v-text-field
                v-model="inputNumber"
                type="number"
                :rules="[range, exist]"
              ></v-text-field>
            </v-form>
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
      <v-btn
        @click="remove"
      >
        取消
      </v-btn>
      <v-dialog
        v-model="resetDialog"
        tile
        width="400"
      >
        <template v-slot:activator="{ on, attrs }">
          <v-btn
            v-bind="attrs"
            v-on="on"
          >
            リセット
          </v-btn>
        </template>

        <v-card>
          <v-card-title>
            すべての入力をリセットしますか？
          </v-card-title>

          <v-card-actions>
            <v-btn
              text
              @click="reset"
            >
              はい
            </v-btn>
            <v-btn
              text
              @click="resetDialog = false"
            >
              いいえ
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
              class="justify-center"
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
      addDialog: false,
      resetDialog: false,
      inputNumber: 0,
      boxNumber,
      numbers: [],
      range: value => (parseInt(value) >= 0 && parseInt(value) <= 200) || '0から200の数字を入力してください',
      exist: value => this.numbers.indexOf(parseInt(value)) === -1 || 'すでに入力されている数字です',
      // ↓上手く機能しない、一度判定入ったら抜け出せなくなる
      // integer: value => Number.isInteger(value) || '整数を入力してください',
    }
  },
  methods: {
    add(value) {
      // メソッド名と処理の不一致感
      // 要リファクタ

      if (this.$refs.form.validate()) {
        this.numbers.push(parseInt(value))
        this.addDialog = false
        this.inputNumber = 0
      }
    },
    remove() {
      this.numbers.pop()
    },
    reset() {
      this.numbers = []
      this.resetDialog = false
    },
  },
  watch: {
    numbers() {
      sessionStorage.setItem('numbers', this.numbers)
    }
  },
  mounted() {
    const numbersData = sessionStorage.getItem('numbers')

    if (!!numbersData) {
      this.numbers = numbersData.split(',').map(value => parseInt(value))
    }
  },
}
</script>

