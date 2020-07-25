<template>
  <div class="container">
    <form>
      <h1>Contato</h1>
      <div class="contato">
        <div class="campos" v-for="(dado, index) in formulario" :key="index">
          <label>{{ dado.title }}</label>
          <input
            :style="{ borderColor: cor }"
            v-model="campos[index]"
            type="text"
            :placeholder="dado.placeholder"
          />
        </div>
        <span v-if="erro">PREENCHA TODOS OS CAMPOS</span>
      </div>
      <label>Telefone</label>
      <input
        :style="{ borderColor: cor }"
        v-model="telefone"
        type="tel"
        placeholder="telefone"
        v-mask="'(##) ####-####'"
      />

      <div>
        <button :style="{ background: cor }" @click="addcampo" type="button">
          Add campo
        </button>
      </div>

      <div>
        <button :style="{ background: cor }" @click="submit" type="button">
          Submit
        </button>
      </div>
    </form>
    <div class="cores">
      <span @click="cor = 'black'"></span>
      <span @click="cor = '#87f'"></span>
      <span @click="cor = 'green'"></span>
    </div>
    <div >
      <DadosCadastrados :campos="campos" />
    </div>
  </div>
</template>

<script>
import DadosCadastrados from "@/components/DadosCadastrados.vue";
export default {
  name: "formulario",
  components: {
    DadosCadastrados,
  },
  data() {
    return {
      cor: "",
      erro: false,
      telefone: "",
      campos: [],
      formulario: [
        {
          title: "Nome",
          placeholder: "nome",
        },
        {
          title: "Email",
          placeholder: "email",
        },
      ],
    };
  },

  methods: {
    addcampo() {
      this.formulario.push({
        title: "QQR",
        placeholder: "qqr",
      });
    },

    submit() {
      let campos = [];
      this.campos.forEach((item) => {
        if (item !== null && item !== "") {
          campos.push(item);
        }
      });
      if (this.formulario.length > campos.length || this.telefone === "") {
        this.erro = true;
        setTimeout(() => {
          this.erro = false;
        }, 1500);
      }
     
      
    },
    
  },
  watch: {
    telefone(){

    }
  }
};
</script>

<style>
.container {
  width: 520px;
  margin: 0 auto;
  padding: 20px;
  box-sizing: border-box;
  background: #c2c2c2;
}

label {
  display: flex;
  flex-direction: row;
}
input {
  display: block;
  width: 100%;
  margin: 10px 0;
  padding: 10px;
  box-sizing: border-box;
  border: 1px solid #87f;
  border-radius: 4px;
}

button {
  display: block;
  width: 100%;
  padding: 10px;
  box-sizing: border-box;
  margin: 10px 0;
  cursor: pointer;
  background: #87f;
  border: none;
  border-radius: 4px;
  color: #ffff;
}

.cores {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
}

.cores span {
  display: inline-block;
  width: 30px;
  height: 30px;
  border-radius: 30px;
  cursor: pointer;
}

span:nth-child(1) {
  background: #000;
}

span:nth-child(2) {
  background: #87f;
}

span:nth-child(3) {
  background: green;
}
</style>
