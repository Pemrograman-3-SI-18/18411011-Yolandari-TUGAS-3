<template>
  <div class="q-pa-md">
    <q-table
      title="Treats"
      :data="data"
      :columns="columns"
      row-key="id"
      :filter="filter"
      :loading="loading"
    >

      <template v-slot:top>
        <span class="text-h5 text-weight-light q-pa-md">
          <span class="text-white-14"> Data Transaksi </span>
        </span>
          <q-space/>
        <q-input borderless dense debounce="300" color="primary" v-model="filter">
          <template v-slot:append>
            <q-icon name="search" />
          </template>
        </q-input>
      </template>

    </q-table>
  </div>
</template>

<script>
export default {
  data () {
    return {
      loading: false,
      filter: '',
      rowCount: 10,
      columns: [
        {
          name: 'desc',
          required: true,
          label: 'Data Transaksi',
          align: 'left',
          field: row => row.kodeTransaksi,
          format: val => `${val}`,
          sortable: true
        },
        { name: 'namaPembeli', align: 'center', label: 'Nama Pembeli', field: 'namaPembeli', sortable: true },
        { name: 'judulBuku', align: 'center', label: 'Judul Buku', field: 'judulBuku', sortable: true },
        { name: 'hargaBuku', lign: 'center', label: 'Harga Buku', field: 'hargaBuku' },
        { name: 'jumlahBeli', lign: 'center', label: 'Jumlah Beli', field: 'jumlahBeli' },
        { name: 'total', lign: 'center', label: 'Total', field: 'total' }

      ],
      data: [
        {
          kodeTransaksi: 'M001',
          namaPembeli: 'Ade Riadi',
          judulBuku: 'Pemograman 3',
          hargaBuku: '150.000',
          jumlahBeli: '5',
          total: '750.000'
        },
        {
          kodeTransaksi: 'M002',
          namaPembeli: 'Nur Aisyah',
          judulBuku: 'Prak. Pemograman 3',
          hargaBuku: '250.000',
          jumlahBeli: '7',
          total: '1.750.000'
        },
        {
          kodeTransaksi: 'M003',
          namaPembeli: 'Yollandari ',
          judulBuku: 'Pemograman 3',
          hargaBuku: '150.000',
          jumlahBeli: '2',
          total: '300.000'
        }
      ]
    }
  },

  methods: {
    // emulate fetching data from server
    addRow () {
      this.loading = true
      setTimeout(() => {
        const
          index = Math.floor(Math.random() * (this.data.length + 1)),
          row = this.original[Math.floor(Math.random() * this.original.length)]
        if (this.data.length === 0) {
          this.rowCount = 0
        }
        row.id = ++this.rowCount
        const addRow = { ...row } // extend({}, row, { name: `${row.name} (${row.__count})` })
        this.data = [...this.data.slice(0, index), addRow, ...this.data.slice(index)]
        this.loading = false
      }, 500)
    },

    removeRow () {
      this.loading = true
      setTimeout(() => {
        const index = Math.floor(Math.random() * this.data.length)
        this.data = [...this.data.slice(0, index), ...this.data.slice(index + 1)]
        this.loading = false
      }, 500)
    }
  }
}
</script>
