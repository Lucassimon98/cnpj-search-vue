<template>
    <div class="container mt-5">
        <div class="card">
            <div class="card-header">
                <h4>
                    CNPJ Search
                </h4>
                <input type="text" v-model="model.cnpjs.cnpjSearch" placeholder="Digite o CNPJ">
                <button type="button" @click="getCnpjs" class="btn btn-primary ms-2">Search</button>
            </div>
            <div class="card-body">
                <table class="table table-board">
                    <thead>
                        <tr>
                            <th>CNPJ</th>
                            <th>Razão Social</th>
                            <th>Nome Fantasia</th>
                            <th>Situação Cadastral</th>
                            <th>Data Inicio</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td>{{ this.model.cnpjs.cnpj }}</td>
                            <td>{{ this.model.cnpjs.razao_social }}</td>
                            <td>{{ this.model.cnpjs.nome_fantasia }}</td>
                            <td>{{ this.model.cnpjs.descricao_situacao_cadastral }}</td>
                            <td>{{ this.model.cnpjs.data_inicio_atividade }}</td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>
</template>
<script>
  import axios from 'axios'
  export default {
    name: 'cnpjSearch',
    data() {
      return{
        model: {
          cnpjs: {
            cnpjSearch: '',
            cnpj: '',
            razao_social: '',
            nome_fantasia: '',
            descricao_situacao_cadastral: '',
            data_inicio_atividade: '',
          }
        }
      }
    },
    methods: {

      
      getCnpjs(cnpj) {
            var cnpj = this.model.cnpjs.cnpjSearch
            axios.get(`https://brasilapi.com.br/api/cnpj/v1/${cnpj}`).then(res => {
                this.model.cnpjs = res.data
                
                console.log(this.model.cnpjs)
            });
        },
    }
  }
</script>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>

