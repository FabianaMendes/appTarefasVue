<template>
  <div id="item">
    <ul>
      <li v-for="task in lista" :key="task.key">
        <span>{{task.text}}</span>
        <button @click="deleteItem(task.key)">Concluir</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'Item', 
  props: [
    'lista',
    'delete'
  ],
  methods: {
    deleteItem(key){
      this.delete(key);
    }
  }
}
</script>

<style scoped>
  #item{
    white-space: pre-wrap;
    word-wrap: break-word;
  }
  ul{
    list-style: none;
    padding: 0;
    margin-top: 20px;
  }
  ul li{
    padding: 15px 0;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
  }
  li:not(:first-child){
    border-top: 1px solid #eee;
  }
  span{
    color: #0D2636;
  }
  button{
    cursor: pointer;
    background-color: #DDD;
    color: #000;
    border: none;
    padding: 8px 10px;
    outline: none;
    border-radius: 4px;
  }
</style>