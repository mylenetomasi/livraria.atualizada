<script>
import { v4 as uuidv4 } from "uuid";
export default {
  data() {
    return {
      categorias: [
        { id: "8ae6623d-5462-4774-b5e1-e263c5d2d367", nome: "romance", classificacao: "qualquer idade"},
        { id: "1f659d91-17b5-40da-b5fb-dbffa5664e27", nome: "ficção" , classificacao: "12 a 30"},
        { id: "d5a59ada-da1d-47a2-9a6e-e99964df9571", nome: "terror" ,  classificacao: "15 a 70" },
        { id: "2311c938-42fa-4661-a3fc-9ba664a30f6e", nome: "suspense" , classificacao: "11 a 50"},
        { id: "6f58a76b-0ea0-4bca-8d93-296c7d69685c", nome: "distopia" ,  classificacao: "14 a 60" },
      ],
      nova_categoria: "",
      nova_classificacao: "",
    };
  },

  methods: {
    salvar() {
      if (this.nova_categoria !== "") {
        const novo_id = uuidv4();
        this.categorias.push({
          id: novo_id,
          nome: this.nova_categoria,
          classificacao: this.nova_classificacao
        });
        this.nova_categoria = ""; 
        this.nova_classificacao = ""; 
      }
    },
    excluir(categorias) {
      const indice = this.categorias.indexOf(categorias);
      this.categorias.splice(indice, 1);
    },
  },
};
</script>

<template>
  <div class="container">
    <div class="title">
      <h2>Gerenciamento de Categorias</h2>
    </div>
    <div class="form-input">
      <input type="text" placeholder="categoria" v-model="nova_categoria" />
      <input type="text" placeholder="classificação" v-model="nova_classificacao" />
      <button @click="salvar">Salvar</button>
    </div>
    <div class="list-categorias">
      <table>
        <thead>
          <tr>
            <th>ID</th>
            <th>Categoria</th>
            <th>Classificação</th>
            <th>Ações</th>       
          </tr>
        </thead>
        <tbody>
          <tr v-for="categoria in categorias" :key="categoria.id">
            <td>{{ categoria.id }}</td>
            <td>{{ categoria.nome }}</td>
            <td>{{ categoria.classificacao }}</td>
            <td>
              <button class="excluir" @click="excluir(categoria)">Excluir</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<style>
.title {
  margin-top: 2rem;
  display: flex;
  justify-content: center;
}
.form-input {
  margin-top: 10px;
  display: flex;
  justify-content: center;
}

.form-input input {
  width: 20%;
  height: 50px;
  border: 1px solid #ccc;
  border-radius: 10px;
  padding: 0 10px;
  margin-left: 20px;
}

.form-input button {
  margin-left: 1%;
  width: 20%;
  height: 40px;
  border: 1px solid rgb(0, 0, 0);
  border-radius: 10px;
  background-color: rgb(0, 0, 0);
  color: white;
  font-weight: bold;
  cursor: pointer;
  
}

.list-categorias {
  display: flex;
  justify-content: center;
}

table {
  width: 50%;
  margin: 2% auto;
  border-collapse: collapse;
}

table tr th {
  border: 1px solid #ccc;
  padding: 10px;
  font-weight: bold;
}

table tr td {
  border: 1px solid #ccc;
  padding: 10px;
}

table tr:nth-child(odd) {
  background-color: black;
}
.excluir{
  background-color: black;
  color: white;
  border:white;
  border-radius: 20px;
  width: 93%;
  height: 30px;
}
</style>