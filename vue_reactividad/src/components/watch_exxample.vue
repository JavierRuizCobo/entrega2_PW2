<template>
  <div>
    <h1>Calculadora con watch</h1>
    <input type="number" v-model="number1" @input="calculateResult">
    <select v-model="operator" @change="calculateResult">
      <option value="+">+</option>
      <option value="-">-</option>
      <option value="*">*</option>
      <option value="/">/</option>
    </select>
    <input type="number" v-model="number2" @input="calculateResult">
    <p>Resultado: {{ result }}</p>
  </div>
</template>

<script setup>
  import { ref, watch } from 'vue';

  const number1 = ref(0);
  const number2 = ref(0);
  const operator = ref('+');
  const result = ref(0);

  function calculateResult(){
    switch (operator.value) {
      case '+':
        result.value = number1.value + number2.value;
        break;
      case '-':
        result.value = number1.value - number2.value;
        break;
      case '*':
        result.value = number1.value * number2.value;
        break;
      case '/':
        result.value = number1.value / number2.value;
        break;
    }
  };

  // Usamos watch para observar cambios en los números y el operador y actualizar el resultado
  watch([number1, number2, operator], () => {
    calculateResult();
  });

</script>
