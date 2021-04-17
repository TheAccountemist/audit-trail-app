<template>
  <div>
    <div class="q-pa-md" style="max-width: 350px">
    <q-list bordered padding>
      <q-item-label header>Audit Trail</q-item-label>
      <q-item-label v-if="values.length === 0" caption>No changes made yet</q-item-label>
      <q-item v-for="(item,idx) in values" :key="idx" class="flex flex-center justify-end">
        <q-item-section avatar>
          <q-item-label caption>row: {{item.rowIndex}}</q-item-label>
          <q-item-label caption>col: {{item.col}}</q-item-label>
        </q-item-section>
        <q-space></q-space>
        <q-item-section>{{formatNumber(item.initialValue)}}
          <q-item-label caption>Initial</q-item-label>
        </q-item-section>
        <q-item-section>{{formatNumber(item.value)}}
          <q-item-label caption>Updated</q-item-label>
        </q-item-section>
      </q-item>

      <!-- <q-separator spaced inset="item" /> -->

    </q-list>
  </div>
  </div>
</template>

<script>
export default {
  props:['values'],
  methods:{
    formatNumber(value){
      const targetValue = +value ? +value : value
      return targetValue.toLocaleString('en-US')
    },
  }
}
</script>

