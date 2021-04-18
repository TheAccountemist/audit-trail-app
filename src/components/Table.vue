<template>  
<div>
  <q-toggle v-model="loading" label="Loading state" class="q-mb-md" />
  <q-table
      title="Transactions"
      :data="data"
      :columns="columns"
      row-key="rowNumber"
      :loading="loading"
  >
      <template v-slot:loading>
        <q-inner-loading showing color="primary" />
      </template>

       <template v-slot:body-cell="props">
          <q-td           
          :props="props"
          >
            {{ props.value }} 
          <q-popup-edit v-model="data[props.rowIndex][props.col.name]" 
              >
          <template v-slot="{ initialValue, value, emitValue, validate, set, cancel }">
          <q-input
            autofocus
            dense
            :value="data[props.rowIndex][props.col.name]"
            hint="Enter value"
            @input="emitValue"
          >
            <template v-slot:after>
              <q-btn flat dense color="negative" icon="cancel" @click.stop="cancel" />
              <q-btn 
              flat 
              dense 
              color="positive" 
              icon="check_circle"
              @focus.stop="storeInput({
                'initialValue':initialValue,
                'value':value,
                'rowIndex':props.rowIndex + 1,
                'col':props.col.name        
                })"
              @click.stop="set" 
              :disable="validate(value) === false || initialValue === value" 
              />
            </template>
          </q-input>
        </template>
          </q-popup-edit>
          </q-td>
      </template>      
  </q-table>
</div>
</template>

<script>
export default {
  data() {
    return {
      columns:[
        { 
          name: 'rowNumber', 
          required: true,
          align: 'left', 
          label: 'Row #', 
          field: row => row.rowNumber,
          sortable: true 
        },
        { name: 'account', align: 'left', label: 'Account', field: 'account', sortable: true },
        { name: 'debit', align: 'left', label: 'Debit', field: 'debit', sortable: true },
        { name: 'credit', align: 'left', label: 'Credit', field: 'credit', sortable: true },
      ],   
      data:[
        {
          rowNumber: 1,
          account: 'Checkings',
          debit: 100,
          credit: 0,
        },
        {
          rowNumber: 2,
          account: 'Savings',
          debit: 1000,
          credit: 0,
        },
        {
          rowNumber: 3,
          account: 'Checkings',
          debit: 0,
          credit: 500,
        },
        {
          rowNumber: 4,
          account: 'Checkings',
          debit: 600,
          credit: 0,
        },
        {
          rowNumber: 5,
          account: 'Savings',
          debit: 1500,
          credit: 0,
        },
        {
          rowNumber: 6,
          account: 'Checkings',
          debit: 0,
          credit: 200,
        },
        {
          rowNumber: 7,
          account: 'Checkings',
          debit: 4500,
          credit: 0,
        },
        {
          rowNumber: 8,
          account: 'Savings',
          debit: 900,
          credit: 0,
        },
        {
          rowNumber: 9,
          account: 'Checkings',
          debit: 0,
          credit: 50,
        },
        {
          rowNumber: 10,
          account: 'Checkings',
          debit: 0,
          credit: 3200,
        },
      ],
      loading:false,
    }
  },
  emits:['storeValues'],
  methods: {
      storeInput(values){
        this.$emit('storeValues',values)

      },
  },
}
</script>


