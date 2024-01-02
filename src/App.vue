<template>
  <div>
    <h1>Calculadora Vue</h1>

    <label for="primeiroNumero">Primeiro Número:</label>
    <input type="number" v-model="primeiroNumero" id="primeiroNumero" @input="recalcularResultado">

    <label for="operacao">Operação:</label>
    <select v-model="operacao" id="operacao" @change="recalcularResultado">
      <option value="soma">+</option>
      <option value="subtracao">-</option>
      <option value="multiplicacao">*</option>
      <option value="divisao">/</option>
    </select>

    <label for="segundoNumero">Segundo Número:</label>
    <input type="number" v-model="segundoNumero" id="segundoNumero" @input="recalcularResultado">

    <p>Resultado: {{ resultado }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      primeiroNumero: 0,
      operacao: 'soma',
      segundoNumero: 0,
    };
  },
  computed: {
    resultado() {
      return this.calcularResultado();
    },
  },
  methods: {
    calcularResultado() {
      const num1 = parseFloat(this.primeiroNumero);
      const num2 = parseFloat(this.segundoNumero);

      switch (this.operacao) {
        case 'soma':
          return num1 + num2;
        case 'subtracao':
          return num1 - num2;
        case 'multiplicacao':
          return num1 * num2;
        case 'divisao':
          return num2 !== 0 ? num1 / num2 : 'Não é possível dividir por zero';
        default:
          return 'Operação inválida';
      }
    },
    recalcularResultado() {
      this.$forceUpdate(); // Força a atualização da visualização
    },
  },
};
</script>

<style scoped>
/* Adicione estilos específicos para este componente */
div {
  background-color: #f0f0f0;
  padding: 20px;
  margin: 20px 0;
}

label {
  display: block;
  margin-bottom: 5px;
}

input,
select {
  margin-bottom: 10px;
}
</style>
