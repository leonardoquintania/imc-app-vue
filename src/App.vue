<template>
  <h1 class="label-title">Calculo do IMC</h1>
  <h2 class="label-subtitle">Digite seu peso e altura para calular o IMC</h2>
  <div class="div-imc">
    <span class="p-float-label">
      <InputText
        id="input-weight"
        type="text"
        v-model="weight"
        :disabled="imc"
      />
      <label for="input-weight">Peso</label>
    </span>
  </div>

  <div class="div-imc">
    <span class="p-float-label">
      <InputText
        id="input-height"
        type="text"
        v-model="height"
        :disabled="imc"
      />
      <label for="input-height">Altura</label>
    </span>
  </div>
  <div class="div-imc" v-if="!imc">
    <Button label="Limpar" @click="clear" />
    <Button style="margin-left: 1rem " label="Calcular" @click="calculate" />
  </div>
  <div class="div-imc" v-if="imc">
    <p class="label-result">Seu IMC é: {{ imc }}</p>
    <p class="label-classification">
      A classificação do seu IMC é: {{ classification }}
    </p>
    <Button label="Calcular novamente" @click="clear" />
  </div>
</template>

<script>
export default {
  data() {
    return {
      height: null,
      weight: null,
      imc: null,
      classification: '',
    };
  },
  methods: {
    calculate: function() {
      this.imc = (this.weight / (this.height * this.height)).toFixed(2);
      this.classification = this.defineClassification(this.imc);
    },
    defineClassification(imc) {
      if (imc < 18.5) {
        return 'Magreza';
      } else if (imc >= 18.5 && imc < 25) {
        return 'Normal';
      } else if (imc >= 25 && imc < 30) {
        return 'Sobrepeso';
      } else if (imc >= 30 && imc < 40) {
        return 'Obesidade';
      } else {
        return 'Obesidade grave';
      }
    },
    clear() {
      this.height = null;
      this.weight = null;
      this.imc = null;
      this.classification = '';
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

.div-imc {
  margin-top: 2rem;
}

.label-title {
  font-size: 2rem;
}

.label-subtitle {
  font-size: 1.1rem;
}

.label-result {
  font-size: 2rem;
}

.label-classification {
  font-size: 1.5rem;
}

button {
  margin-right: 1rem;
}
</style>
