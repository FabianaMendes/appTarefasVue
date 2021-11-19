<template>
  <div id="task">
    <form @submit.prevent="addTarefa">
      <input
        type="text"
        placeholder="Tarefa de hoje?"
        v-model="tarefa"
      />
      <button type="submit">Adicionar</button>
    </form>

    <Item :lista="tarefas" :delete="deleteTask"/>

    <span v-show="tarefas.length > 0">
      Você tem <b :class="{pend: pendente}">{{tarefas.length}}</b> tarefas pendentes
    </span>
  </div>
</template>

<script>
import Item from './Item.vue';

export default{
  name: 'Task',
  components: {
    Item,
  },
  data(){
    return{
      tarefa: '',
      tarefas: [],
      pendente: false,
    }
  },
  methods:{
    addTarefa(){
      if(this.tarefa !== ''){
        this.tarefas.push({
          text: this.tarefa,
          key: Date.now(),
        });
      }else{
        alert('Digite uma tarefa!');
        return;
      }
      this.tarefa = '';
    },
    deleteTask(key){
      let filtro = this.tarefas.filter((item)=> {
        return (item.key !== key);
      });
      return this.tarefas = filtro;
    },
  },
  watch: {
    tarefas:{
      deep: true,
      handler(){
        localStorage.setItem('tasks', JSON.stringify(this.tarefas));
        this.tarefas.length > 4 ? this.pendente = true : this.pendente = false;
      }
    }
    //tarefas(){
    //  localStorage.setItem('tasks', JSON.stringify(this.tarefas));
    //}
  },
  created(){ //É chamado automaticamente após a instancia do Vue ser criada...
    const storagedTasks = localStorage.getItem('tasks');
    this.tarefas = JSON.parse(storagedTasks) || [];
  }
}
</script>

<style scoped>
  #task{
    max-width: 700px;
    background-color: #FFF;
    border-radius: 4px;
    padding: 20px;
    margin: 20px auto;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.3);
  }
  form{
    margin-top: 30px;
    display: flex;
    flex-direction: row;
  }
  form button{
    cursor: pointer;
    background-color: #FFB100;
    border: none;
    border-radius: 4px;
    margin-left: 10px;
    padding: 5px 15px;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  input{
    flex: 1;
    border: 1px solid #eee;
    padding: 6px 10px;
    border-radius: 4px;
    font-size: 14px;
    outline: none;
  }
  .pend{
    color: #FF0000;
  }
</style>