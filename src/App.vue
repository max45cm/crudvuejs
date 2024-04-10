<template>
  <div class="container">
    <h1>Confeitaria</h1>
    <div class="form-container">
      <div class="form-group">
        <label for="tipo">Tipo:</label>
        <input type="text" v-model="novoBolo.tipo">
      </div>
      <div class="form-group">
        <label for="massa">Massa:</label>
        <input type="text" v-model="novoBolo.massa">
      </div>
      <div class="form-group">
        <label for="recheio">Recheio:</label>
        <input type="text" v-model="novoBolo.recheio">
      </div>
      <div class="form-group">
        <label for="cobertura">Cobertura:</label>
        <input type="text" v-model="novoBolo.cobertura">
      </div>
      <div class="form-group">
        <label for="preco">Preço:</label>
        <input type="text" v-model="novoBolo.preco">
      </div>
      <button class="btn-primary" @click="adicionarOuEditarBolo">{{ modoEdicao ? 'Editar' : 'Adicionar' }}</button>
    </div>

    <h2>Bolos Adicionados</h2>
    <div class="table-container">
      <table>
        <thead>
          <tr>
            <th>Tipo</th>
            <th>Massa</th>
            <th>Recheio</th>
            <th>Cobertura</th>
            <th>Preço</th>
            <th>Ações</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(bolo, index) in bolos" :key="index" :class="{'table-row-hover': !modoEdicao}">
            <td>{{ bolo.tipo }}</td>
            <td>{{ bolo.massa }}</td>
            <td>{{ bolo.recheio }}</td>
            <td>{{ bolo.cobertura }}</td>
            <td>{{ bolo.preco }}</td>
            <td>
              <button class="btn-edit" @click="preencherCamposEdicao(index)">Editar</button>
              <button class="btn-delete" @click="excluirBolo(index)">Excluir</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      bolos: [],
      novoBolo: {
        tipo: '',
        massa: '',
        recheio: '',
        cobertura: '',
        preco: ''
      },
      indiceEdicao: -1
    };
  },
  computed: {
    modoEdicao() {
      return this.indiceEdicao !== -1;
    }
  },
  methods: {
    adicionarOuEditarBolo() {
      if (
        this.novoBolo.tipo &&
        this.novoBolo.massa &&
        this.novoBolo.recheio &&
        this.novoBolo.cobertura &&
        this.novoBolo.preco
      ) {
        if (this.indiceEdicao === -1) {
          this.bolos.push({ ...this.novoBolo });
        } else {
          this.bolos[this.indiceEdicao] = { ...this.novoBolo };
          this.indiceEdicao = -1;
        }
        this.limparCampos();
      } else {
        alert("Por favor, preencha todos os campos.");
      }
    },
    preencherCamposEdicao(index) {
      this.indiceEdicao = index;
      this.novoBolo = { ...this.bolos[index] };
    },
    limparCampos() {
      this.novoBolo = {
        tipo: '',
        massa: '',
        recheio: '',
        cobertura: '',
        preco: ''
      };
    },
    excluirBolo(index) {
      this.bolos.splice(index, 1);
    }
  }
};
</script>

<style scoped>
.container {
  width: 90%; 
  max-width: 1000px; 
  margin: 0 auto; 
  padding: 20px;
  background-color: #333;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 1);
  color: #fff;
}

h1, h2 {
  text-align: center;
}

.form-container {
  margin-bottom: 5px;
}

.form-group {
  margin-bottom: 15px;
}

label {
  display: block;
  font-weight: bold;
}

input[type="text"] {
  width: calc(100% - 10px);
  padding: 8px;
  border: 1px solid #666;
  border-radius: 4px;
  box-sizing: border-box;
  color: #333;
}

button {
  padding: 10px 20px;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
  color: #fff;
}

.btn-primary {
  background-color: #757575;
  border: none;
}

.btn-primary:hover {
  background-color: #5a5a5a;
}

.btn-edit, .btn-delete {
  background-color: #757575;
  border: none;
}

.btn-edit:hover, .btn-delete:hover {
  background-color: #5a5a5a;
}

.table-container {
  overflow-x: auto;
}

table {
  width: 100%;
  border-collapse: collapse;
}

th, td {
  padding: 8px;
  text-align: left;
  border-bottom: 1px solid #ddd;
}

th {
  background-color: #757575;
}

tr:hover {
  background-color: #555;
}

.table-row-hover:hover {
  background-color: transparent;
}
</style>
