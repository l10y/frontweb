<template>
  <v-form>
    <v-container fluid>
      <v-layout row wrap>
        <v-flex xs12 sm1>
          <v-menu ref="monthMenu" :close-on-content-click="false" v-model="monthMenu"
              :return-value.sync="month" lazy transition="scale-transition" offset-y full-width>
            <v-text-field color="green" slot="activator" v-model="formatMonth" label="基準月" readonly></v-text-field>
            <v-date-picker v-model="month" color="green" type="month"
                no-title scrollable @change="$refs.monthMenu.save(month)">
            </v-date-picker>
          </v-menu>
        </v-flex>
        <v-flex xs6 sm2>
          <v-text-field v-model="startedAt" color="green" label="出社時間" type="time"></v-text-field>
        </v-flex>
        <v-flex xs6 sm2>
          <v-text-field v-model="endedAt" color="green" label="退社時間" type="time"></v-text-field>
        </v-flex>
        <v-flex xs12 sm5>
          <v-text-field color="green" label="作業内容" v-model="workingText"></v-text-field>
        </v-flex>
        <v-flex xs12 sm2 right>
          <v-btn large dark color="green" @click="batchEntry">
            一括登録
          </v-btn>
        </v-flex>
      </v-layout>
    </v-container>
  </v-form>
</template>

<script>
  export default {
    data: () => ({
      month: '',
      startedAt: '',
      endedAt: '',
      workingText: '',
      monthMenu: false
    }),
    created() {
      this.month = this.$moment().format('YYYY/MM');
    },
    computed: {
      formatMonth() {
        return this.month.replace('-', '/');
      }
    },
    methods: {
      batchEntry: function() {
        this.$emit('setDefault', this.month, this.startedAt, this.endedAt, this.workingText);
      },
      allowedStep: function(m) {
        return m % 30 === 0;
      }
    }
  }
</script>
