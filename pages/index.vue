<template>
  <v-row justify="center" align="center">
    <v-col cols="3" v-for="index in 100" :key="index">
      <v-card>
        <v-card-text>{{ index }}</v-card-text>
        <v-card-title
          v-if="!!numbers[index - 1]"
        >
          {{ numbers[index - 1] }}
        </v-card-title>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  data() {
    return {
      numbers: [],
    }
  },
  mounted() {
  },
}
</script>

