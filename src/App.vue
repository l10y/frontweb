<template>
  <v-app id="inspire">
    <v-toolbar :color="mainColot" dark fixed app>
      <v-toolbar-title>Attendance</v-toolbar-title>
    </v-toolbar>

    <v-content>
      <default-entry @setDefault="setDefault"></default-entry>
      <v-form>
        <v-container fluid>
          <daily-report v-for="date in dateList" :key="date" :date="date" :defaultStartedAt="defaultStartedAt"
              :defaultEndedAt="defaultEndedAt" :defaultWorkingText="defaultWorkingText"></daily-report>
        </v-container>
      </v-form>
    </v-content>

    <v-footer :color="mainColot" app></v-footer>
  </v-app>
</template>

<script>
  import DefaultEntry from './components/default-entry.vue';
  import DailyReport from './components/daily-report.vue';
import { format } from 'path';

  export default {
    data: () => ({
      mainColot: 'light-green',
      dateList: [],
      defaultStartedAt: null,
      defaultEndedAt: null,
      defaultWorkingText: ''
    }),
    props: {
      source: String
    },
    methods: {
      setDefault: function(month, startedAt, endedAt, workingText) {
        this.dateList = this.getDateList(month);
        this.defaultStartedAt = startedAt;
        this.defaultEndedAt = endedAt;
        this.defaultWorkingText = workingText;

        // this.$axios.post('/working_times', {
        //   started_at: this.$moment(startedAt, 'HH:mm').format(),
        //   ended_at: this.$moment(endedAt, 'HH:mm').format()
        // })
        // .then(function(res) {
        //   console.log(res);
        // })
        // .catch(function(error) {
        //   console.log(error);
        // });
      },
      getDateList: function(month) {
        const moment = this.$moment(month, 'YYYY/MM');
        let from = moment.clone().set('D', '21');
        const to = moment.clone().add(1, 'M').set('D', '20');
        let result = [];
        while (from.isSameOrBefore(to)) {
          result.push(from.format('MM/DD'));
          from.add(1, 'd');
        }
        return result;
      }
    },
    components: {
      'default-entry': DefaultEntry,
      'daily-report': DailyReport
    }
  }
</script>
