<template>
  <div class="container">
    <label>ID</label>
    <input
      type="text"
      v-model="pessoa.id"
      class="form-control"
      placeholder="ID"
    />

    <br />

    <label>Nome</label>
    <input
      type="text"
      v-model="pessoa.nome"
      class="form-control"
      placeholder="Nome"
    />

    <br />

    <label>CPF</label>
    <input
      type="text"
      v-model="pessoa.cpf"
      class="form-control"
      placeholder="CPF"
    />

    <br />

    <label>Telefone</label>
    <input
      type="text"
      v-model="pessoa.telefone"
      class="form-control"
      placeholder="Telefone"
    />

    <br />

    <label>CEP</label>
    <input
      type="text"
      v-model="pessoa.cep"
      class="form-control"
      placeholder="CEP"
    />

    <br />

    <label>Cidade</label>
    <input
      type="text"
      v-model="pessoa.cidade"
      class="form-control"
      placeholder="Cidade"
    />

    <br />

    <button type="submit" class="btn btn-primary" @click="save">
      Salvar
    </button>

    <button type="submit" class="btn btn-primary" @click="searchData">
      Buscar
    </button>

    <button type="submit" class="btn btn-primary" @click="deleteData">
      Deletar
    </button>

  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "PessoaCrud",
  data() {
    return {
      pessoa: {
        id: undefined,
        nome: "",
        cpf: "",
        telefone: "",
        cep: "",
        cidade: "",
      },
    };
  },
  created() {
    this.PessoaLoad();
  },
  methods: {
    PessoaLoad() {
      axios.get("http://localhost:8090/pessoas").then(({ data }) => {
        console.log(data);
        this.result = data;
      });
    },

    save() {
      if (this.pessoa.id == "" || this.pessoa.id == undefined) {
        this.saveData();
      } else {
        this.updateData();
      }
    },

    saveData() {
      console.log(this.pessoa);
      axios
        .post("http://localhost:8090/pessoas", this.pessoa)
        .then(({ data }) => {
          alert("Salvo");
          console.log(data);
        });
    },

    updateData() {
      this.pessoa.id = parseInt(this.pessoa.id);
      axios
        .put("http://localhost:8090/pessoas", this.pessoa)
        .then(({ data }) => {
          alert("Atualizado");
          console.log(data);
        });
    },

    searchData() {
      console.log("ajohbdsaikujydfgvsaksjdgvasujkyv");
      axios
        .get(`http://localhost:8090/pessoas/${parseInt(this.pessoa.id)}`)
        .then(({ data }) => {
          console.log(data);
        });
    },

    deleteData() {
      axios
        .delete(`http://localhost:8090/pessoas/${parseInt(this.pessoa.id)}`)
        .then(({ data }) => {
          console.log(data);
        });
    },
  },
};
</script>