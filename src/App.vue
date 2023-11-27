<template>
  <div class="stock-trading-container">
    <h2 class="header">Jual Beli Saham</h2>
    <div class="stock-info">
      <p>Jumlah Lembar Saham: {{ jumlahSaham }}</p>
      <p>Harga per Lembar Saham: {{ formatCurrency(hargaSaham) }}</p>
      <p>Total Nilai Saham Dimiliki: {{ formatCurrency(totalNilaiSaham) }}</p>
    </div>
    <div class="stock-buttons">
      <button @click="beliSaham" class="tombol-beli">Beli Saham (1 lot)</button>
      <button @click="jualSaham" :disabled="jumlahSaham === 0" class="tombol-jual">Jual Saham (1 lot)</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      jumlahSaham: 0,
      hargaSaham: 500, // Harga saham awal
    };
  },
  computed: {
    totalNilaiSaham() {
      return this.jumlahSaham * this.hargaSaham;
    },
  },
  methods: {
    beliSaham() {
      this.jumlahSaham += 100;
    },
    jualSaham() {
      if (this.jumlahSaham > 0) {
        this.jumlahSaham -= 100;
      }
    },
    formatCurrency(value) {
      return new Intl.NumberFormat('id-ID', { style: 'currency', currency: 'IDR' }).format(value);
    },
  },
};
</script>

<style scoped>
.stock-trading-container {
  max-width: 400px;
  margin: 20px auto;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 8px;
  background-color: #f9f9f9;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.header {
  color: #333;
}

.stock-info {
  margin-bottom: 20px;
}

.stock-buttons {
  display: flex;
  justify-content: space-between;
}

.tombol-beli,
.tombol-jual {
  padding: 10px;
  font-size: 14px;
  cursor: pointer;
  background-color: #4caf50;
  color: #fff;
  border: none;
  border-radius: 4px;
  transition: background-color 0.3s;
}

.tombol-jual:disabled {
  background-color: #aaa;
  cursor: not-allowed;
}
</style>
