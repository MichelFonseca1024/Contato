<template>
  <section>
    <div class="form" v-for="(formulario, key, index) in formularios" :key="index">
      <div class="campos" v-for="(campo, nome, index) in formulario" :key="index">
        <div>{{ nome }}</div>
        <div>{{ campo }}</div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "dadosCadastrados",
  data() {
    return {
      formularios: "",
    };
  },
  methods: {
    pegarFormularios() {
      this.formularios = this.$store.state.formularios;
    },
  },
  created() {
    this.formularios = this.$store.state.formularios;
  },
};
</script>

<style scoped>
.form {
  background: #fff;
  border-radius: 4px;
  margin: 20px 0;
  box-sizing: border-box;
  padding: 15px;
}

.campos {
  display: grid;
  grid-template-columns: 1fr 2fr;
  line-height: 40px;
  border-bottom: 1px solid #c2c2c2;
}

.campos :nth-child(1) {
  text-transform: capitalize;
  text-align: center;
}
</style>
