<template>
  <v-layout row wrap>
    <v-flex xs12 sm1>
      <v-text-field single-line outline v-model="date" color="green" readonly tabindex="-1"></v-text-field>
    </v-flex>
    <v-flex xs6 sm2>
      <v-text-field single-line outline v-model="startedAt" color="green" type="time"></v-text-field>
    </v-flex>
    <v-flex xs6 sm2>
      <v-text-field single-line outline v-model="endedAt" color="green" type="time"></v-text-field>
    </v-flex>
    <v-flex xs12 sm5>
      <v-text-field single-line outline v-model="workingText" color="green"></v-text-field>
    </v-flex>
  </v-layout>
</template>

<script>
  export default {
    props: {
      date: String,
      defaultStartedAt: String,
      defaultEndedAt: String,
      defaultWorkingText: String
    },
    data: () => ({
      startedAt: '',
      endedAt: '',
      workingText: ''
    }),
    mounted() {
      this.startedAt = this.defaultStartedAt;
      this.endedAt = this.defaultEndedAt;
      this.workingText = this.defaultWorkingText;
    },
    watch: {
      defaultStartedAt() {
        this.startedAt = this.defaultStartedAt;
      },
      defaultEndedAt() {
        this.endedAt = this.defaultEndedAt;
      },
      defaultWorkingText() {
        this.workingText = this.defaultWorkingText;
      }
    }
  }
</script>
