<template>
  <q-page class="flex flex-center">
    <div class="q-pa-md" style="max-width: 300px">
      <q-input filled v-model="date" mask="date" :rules="['date']">
        <template v-slot:append>
          <q-icon name="event" class="cursor-pointer">
            <q-popup-proxy ref="qDateProxy" transition-show="scale" transition-hide="scale">
              <q-date v-model="date" @input="() => $refs.qDateProxy.hide()" />
            </q-popup-proxy>
          </q-icon>
        </template>
      </q-input>
    </div>
    <div class="table">
      <div class="table-row row" v-for="(list, index) in learnPlanList" :key="index">
        <div class="table-cell q-pa-sm" v-for="(item, index) in list" :key="index">{{item}}</div>
      </div>
    </div>
  </q-page>
</template>

<script>
import { date } from 'quasar'
const { formatDate } = date

export default {
  name: 'learnPlanPageIndex',
  data () {
    return {
      date: new Date(),
      learnPlanList: []
    }
  },
  methods: {
    loadPlanList () {
      this.$axios.get('http://118.25.97.247/api/tools/ebbinghaus', {
        params: {
          start_date: formatDate(new Date(), 'YYYY-MM-DD'),
          days: 14
        }
      })
        .then(res => {
          this.learnPlanList = res.data
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
<style lang="stylus">
.table
  border 1px solid $accent
  .table-row
    &:not(:last-child)
      border-bottom 1px solid $primary
    .table-cell
      &:not(:last-child)
        border-right 1px solid $positive
</style>
