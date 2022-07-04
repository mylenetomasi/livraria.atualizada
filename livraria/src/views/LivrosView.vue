<script>
import { v4 as uuidv4 } from "uuid";
export default {
  data() {
    return {
      livros: [
        { id: "8ae6623d-5462-4774-b5e1-e263c5d2d367", nome: "Livro 1",ISBN:"978-65-5941-167-2" , quantidade: "2", preco: "109,90" },
        { id: "1f659d91-17b5-40da-b5fb-dbffa5664e27", nome: "Livro 2",ISBN:"738-73-8375-738-3", quantidade: "10", preco:"459,99" },
        { id: "d5a59ada-da1d-47a2-9a6e-e99964df9571", nome: "Livro 3",ISBN:"476-74-5941-830-5", quantidade: "5", preco:"350,00" },
        { id: "2311c938-42fa-4661-a3fc-9ba664a30f6e", nome: "Livro 4",ISBN:"748-93-7498-169-8", quantidade: "1", preco:"20,70" },
        { id: "6f58a76b-0ea0-4bca-8d93-296c7d69685c", nome: "Livro 5",ISBN:"027-84-8953-843-7", quantidade: "20", preco:"659,00" },
      ],
      novo_livro: "",
      novo_ISBN: "",
      novo_preco:"",
      nova_quantidade:"",
    };
  },

  methods: {
    salvar() {
      if (this.novo_livro !== "") {
        const novo_id = uuidv4();
        this.livros.push({
          id: novo_id,
          nome: this.novo_livro,
          ISBN:this.novo_ISBN,
          preco: this.novo_preco,
          quantidade: this.nova_quantidade,
        });
        this.novo_livro = "";
        this.novo_ISBN = "";
        this.novo_preco = "";
        this.nova_quantidade = "";
      }
    },
    excluir(Livro) {
      const indice = this.livros.indexOf(Livro);
      this.livros.splice(indice, 1);
    },
  },
};
</script>

<template>
  <div class="container">
    <div class="title">
      <h2>Gerenciamento de Livros</h2>
    </div>
    <div class="form-input">
      <input type="text" placeholder="Nome" v-model="novo_livro" />
      <input type="texto" placeholder="ISBN" v-model="novo_ISBN" />
      <input type="number" placeholder="Quantidade" v-model="nova_quantidade" />
      <input type="number" placeholder="Preço" v-model="novo_preco" />
      <button @click="salvar">Salvar</button>
    </div>
    <div class="list-livros">
      <table>
        <thead>
          <tr>
            <th>ID</th>
            <th>Título</th>
            <th>ISBN</th>
            <th>Quantidade</th>
            <th>Preço</th>
            <th>Ações</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="livro in livros" :key="livro.id">
            <td>{{ livro.id }}</td>
            <td>{{ livro.nome }}</td>
            <td>{{ livro.ISBN}}</td>
            <td>{{ livro.quantidade }}</td>
            <td>{{ livro.preco }}</td>
            <td>
              <button class="excluir" @click="excluir(livro)">Excluir</button>
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
  width: 30%;
  height: 40px;
  border: 1px solid #ccc;
  border-radius: 10px;
  padding: 0 10px;
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


.list-editoras {
  display: flex;
  justify-content: center;
}

table {
  width: 80%;
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
  background-color: #ccc;
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
