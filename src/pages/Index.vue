<template>
  <q-page class="flex flex-center">
    hahaha
  </q-page>
</template>

<script>
import { date } from 'quasar'
const { formatDate } = date

export default {
  name: 'PageIndex',
  data () {
    return {
      learnPlanList: []
    }
  },
  methods: {
    loadPlanList () {
      this.$axios.get('http://118.25.97.247/api/tools/ebbinghaus', {
        params: {
          start_date: formatDate(new Date(), 'YYYY-MM-DD'),
          days: 7
        }
      })
        .then(res => {
          console.log(res)
        })
        .catch(err => {
          console.log(err)
        })
    }
  },
  mounted () {
    this.loadPlanList()
  }
}
</script>
