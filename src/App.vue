<template>
  <div id="app">
    <h1>个人所得税计算器</h1>
    <div class="input-group">
      <input v-model="income" type="number" placeholder="请输入税前收入" />
      <button @click="calculateTax">计算税额</button>
    </div>
    
    <div v-if="result">
      <h2>计算结果</h2>
      <p>应缴税额: <strong>{{ result.tax.toFixed(2) }} 元</strong></p>
      <p>税后收入: <strong>{{ result.netIncome.toFixed(2) }} 元</strong></p>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      income: null,
      result: null,
    };
  },
  methods: {
    calculateTax() {
      axios.post('http://localhost:8081/api/calculateTax', {
        income: this.income,
      })
      .then(response => {
        this.result = response.data;
      })
      .catch(error => {
        console.error('计算税额时出错:', error);
      });
    },
  },
};
</script>

<style>
/* 添加样式以美化界面 */
#app {
  text-align: center;
  margin: 20px;
}

.input-group {
  margin-bottom: 20px;
}

input {
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  margin-right: 10px;
}

button {
  padding: 10px 15px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  background-color: #45a049;
}
</style>
