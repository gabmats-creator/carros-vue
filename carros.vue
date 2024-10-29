<template>
    <div class="carros-container">
      <h2>Cadastro de Carros</h2>
      <div class="form-container">
        <label for="modelo">Modelo:</label>
        <input v-model="novoCarro.modelo" type="text" placeholder="Digite o modelo do carro" required />
        
        <label for="ano">Ano:</label>
        <input v-model="novoCarro.ano" type="number" placeholder="Digite o ano" min="1900" max="2100" required />
        
        <label for="cor">Cor:</label>
        <input v-model="novoCarro.cor" type="text" placeholder="Digite a cor" required />
        
        <button @click="adicionarCarro">Cadastrar Carro</button>
      </div>
  
      <div class="carro-lista">
        <p v-if="carros.length === 0" class="empty-message">Nenhum carro cadastrado.</p>
        <div v-else>
          <div v-for="(carro, index) in carros" :key="index" class="carro-item">
            <span>{{ carro.modelo }} ({{ carro.ano }}) - {{ carro.cor }}</span>
            <button @click="deletarCarro(index)">Deletar</button>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        novoCarro: {
          modelo: '',
          ano: '',
          cor: ''
        },
        carros: []
      };
    },
    methods: {
      adicionarCarro() {
        this.carros.push({ ...this.novoCarro });
  
        this.limparCampos();
      },
      deletarCarro(index) {
        this.carros.splice(index, 1);
      },
      limparCampos() {
        this.novoCarro = { modelo: '', ano: '', cor: '' };
      }
    }
  };
  </script>
  
  <style scoped>
  .carros-container { font-family: Arial, sans-serif; padding: 20px; }
  .form-container { margin-bottom: 20px; }
  .form-container input, button { margin: 5px 0; padding: 8px; }
  .carro-lista { margin-top: 20px; }
  .carro-item { display: flex; justify-content: space-between; margin: 5px 0; padding: 10px; border: 1px solid #ddd; }
  .empty-message { color: #888; }
  </style>
  