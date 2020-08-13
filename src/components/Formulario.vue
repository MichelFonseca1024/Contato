<template>
  <div class="container">
    <form>
      <h1>Contato</h1>
      <div class="contato">
        <div class="campos" v-for="(dado, index) in formulario" :key="index">
          <label>{{ dado.title }}</label>
          <input
            :style="{ borderColor: cor }"
            v-model="campos[dado.title]"
            type="text"
            :placeholder="dado.placeholder"
          />
        </div>
      </div>
      <label>Telefone</label>
      <input
        :style="{ borderColor: cor }"
        v-model="telefone"
        type="tel"
        placeholder="Insira seu telefone"
        v-mask="'(##) ####-####'"
      />

      <div>
        <div class="erro" v-if="erro">PREENCHA TODOS OS CAMPOS!</div>
        <p>Adcionar novo campo (Titulo do campo)</p>
        <input :style="{ borderColor: cor }" type="text" v-model="novoCampo" />
        <button :style="{ background: cor }" @click="addcampo" type="button">Add campo</button>
      </div>

      <div>
        <button :style="{ background: cor }" @click="submeter" type="button">Submit</button>
      </div>
    </form>

    <div class="cores">
      <span @click="cor = 'black'"></span>
      <span @click="cor = '#87f'"></span>
      <span @click="cor = 'green'"></span>
    </div>
    <div>
      <DadosCadastrados />
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
      novoCampo: "",
      cor: "",
      erro: false,
      telefone: "",
      campos: {},
      formulario: [
        {
          title: "nome",
          placeholder: "Digite seu nome",
        },
        {
          title: "email",
          placeholder: "Digite seu  e-mail",
        },
      ],
    };
  },

  methods: {
    addcampo() {
      if (this.novoCampo !== "") {
        this.formulario.push({
          title: this.novoCampo,
          placeholder: this.novoCampo.toLowerCase(),
        });
      }

      this.novoCampo = "";
    },
    submeter() {
      let campos = {};
      Object.keys(this.campos).forEach((item) => {
        if (this.campos[item] !== null && this.campos[item] !== "") {
          campos[item] = this.campos[item];
        }
      });
      if (
        this.formulario.length > Object.keys(campos).length ||
        this.telefone === ""
      ) {
        this.erro = true;
        setTimeout(() => {
          this.erro = false;
        }, 1500);
      } else {
        this.campos["telefone"] = this.telefone;
        this.$store.commit("adcionarFormulario", this.campos);
        this.campos = {};
        this.telefone = "";
      }
    },
  },
};
</script>

<style>
.container {
  width: 600px;
  margin: 0 auto;
  padding: 20px;
  box-sizing: border-box;
  background: #4fc08d;
  border-radius: 4px;
}

label {
  font-weight: bold;
  display: flex;
  flex-direction: row;
  text-transform: capitalize;
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

.erro {
  color: red;
  font-size: 0.9rem;
  text-align: center;
}

.cores span:nth-child(1) {
  background: #000;
}

.cores span:nth-child(2) {
  background: #87f;
}

.cores span:nth-child(3) {
  background: green;
}

@media screen and (max-width: 620px) {
  .container {
    width: 100%;
  }
}
</style>
