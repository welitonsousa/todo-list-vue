<template>
  <div>
    <span class="progress">
      <span :style="`width: ${porcentagem}%`" class="porcentagem">
        <h3 class="numeroPorcentagem">{{ porcentagem }}%</h3>
      </span>
    </span>
    <div>
      <b-input-group class="novaTarefa" size="lg">
        <b-form-input
          @keyup.enter.stop.prevent="add"
          class="corFundo"
          placeholder="Tarefa"
          v-model="tarefaDigitada"
        ></b-form-input>
        <b-input-group-append>
          <b-button variant="success" @click.stop.prevent="add">+</b-button>
        </b-input-group-append>
      </b-input-group>
    </div>
    <div>
      <div class="container wrap">
        <div
          v-for="(element, index) in tarefas"
          :class="{ item: !element.status, item2: element.status }"
          :key="element.nome"
          @click.stop.prevent="changeStatus(index)"
        >
          {{ element.nome }}
          <b-button
            @click.stop.prevent="deleteItem(index)"
            variant="danger"
            class="btDeletar"
            >x</b-button
          >
        </div>
      </div>
    </div>
    <div href="#" id="foo"></div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tarefaDigitada: "",
      tarefas: [],
    };
  },
  created() {
    this.tarefas = localStorage.tarefas ? JSON.parse(localStorage.tarefas) : [];
  },
  computed: {
    porcentagem() {
      const { tarefas } = this;
      const len = tarefas.length;
      const concluida = tarefas.filter((element) => element.status).length;
      
      return len !== 0 ? parseInt((concluida * 100) / len, 10) : 0;
    },
  },
  watch: {
    tarefas: {
      deep: true,
      handler() {
        localStorage.setItem("tarefas", JSON.stringify(this.tarefas));
      },
    },
  },
  methods: {
    deleteItem(index) {
      this.tarefas.splice(index, 1);
    },
    changeStatus(index) {
      this.tarefas[index].status = !this.tarefas[index].status;
    },
    add() {
      const valor = this.tarefas.every(
        (element) => element.nome !== this.tarefaDigitada
      );
      if (valor) {
        this.tarefas.push({ nome: this.tarefaDigitada, status: false });
        window.location.href = "#foo";
      }
      this.tarefaDigitada = "";
    },
  },
};
</script>
<style scoped>
.item .btDeletar {
  border-color: #fff;
}
.btDeletar {
  float: right;
  border-radius: 40px;
  padding: 3px 10px;
}
.numeroPorcentagem {
  padding: 0 24pc;
  color: #fff;
}
.wrap {
  flex-wrap: wrap;
}
.porcentagem {
  background-color: #28a745;
}
.container {
  margin: 0 auto;
  display: flex;
  width: 1500px;
}
.progress {
  border-style: solid;
  border-color: #fff;
  margin-left: auto;
  margin-right: auto;
  width: 60%;
  margin-top: 100px;
  height: 30px;
  border-radius: 5px;
  border-width: 1px;
  background-color: rgb(58, 96, 115);
}
.item {
  min-width: 27%;
  flex: 1;
  margin: 15px 35px;
  padding: 40px;
  background: rgb(223, 54, 25);
  text-align: center;
  font-size: 1.5em;
  border-radius: 10px;
  border-style: solid;
  border-width: 20px;
  color: #fff;
  border-color: rgb(189, 36, 9);
  border-bottom: 0;
  border-top: 0;
  border-right: 0;
}
.item2 {
  min-width: 27%;
  flex: 1;
  margin: 15px 35px;
  padding: 40px;
  background: #28a745;
  text-align: center;
  font-size: 1.5em;
  border-radius: 10px;
  border-style: solid;
  border-width: 20px;
  color: #fff;
  border-color: #11862d;
  border-bottom: 0;
  border-top: 0;
  border-right: 0;
}

.novaTarefa {
  width: 500px !important;
  margin-left: auto;
  margin-right: auto;
  margin-top: 30px;
}
#foo {
  margin-top: 20px;
}
</style>
