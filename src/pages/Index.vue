<template>
  <q-page class="flex justify-center items-start q-gutter-xl q-pt-xl">
    <Table
    @storeValues="storeValues">      
    </Table>
    <Trail
    :values="values"
    />
  </q-page>
</template>

<script>
import Table from '../components/Table'
import Trail from '../components/Trail'
export default {
  name: 'PageIndex',
  components:{
    Table,
    Trail,
  },
  data() {
    return {
      values:[]
    }
  },
  methods: {
    storeValues(values){
      this.values.push(values)
    }
  },
}
</script>


