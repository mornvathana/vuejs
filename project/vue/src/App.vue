<script setup>
  // export default{
  //   data(){
  //     return {
  //       name: 'Jonh',
  //       status: true,
  //       status1: 'active',
  //       tasks: ['test1','test2'],
  //       link: 'https://chatgpt.com/c/67ea0af1-3cdc-800f-a52d-d4e8233f5d90',
  //     }
  //   },
  //   methods: {
  //     ToggleStatus(){
  //       if(this.status1 === 'active' ){
  //         this.status1 = 'pedding';
  //       }else if(this.status1 === 'pedding'){
  //         this.status1 = 'inactive';
  //       }else{
  //         this.status1 = 'active';
  //       }
  //     },
  //   },
  // }
  import { onMounted, ref } from 'vue';


      const name = ref('vathana');
      const status1 = ref('active');
      const tasks = ref(['task1','task2','task3']);

      const newTask = ref('adfsdf');
      const ToggleStatus = () =>{
        if(status1.value === 'active' ){
         status1.value = 'pedding';
        }else if(status1.value === 'pedding'){
          status1.value = 'inactive';
        }else{
          status1.value = 'active';
        }
      }

      const addTask = () =>{
        if(newTask.value.trim() !== ''){
          tasks.value.push(newTask.value);
          newTask.value = '';
        }
      }
      const deleteTask = (index) =>{
        tasks.value.splice(index,1);
      }

      onMounted(async () => {
        try {
            const response = await fetch('https://jsonplaceholder.typicode.com/todos');
            const data = await response.json();
            tasks.value = data.map((task) => task.title)
        } catch (error) {
            console.log('Error fetching api');
        }
        });
</script>
<template>
  <h1>{{ name }}</h1>
  <p v-if="status">true</p>
  <p v-else>not</p>
  <p v-if="status1 === 'active'">active</p>
  <p v-if="status1 === 'pedding'">pedding</p>

  <form @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <input type="text" id = "newTask" name = "newTask" v-model = "newTask">
    <button type = "submit">Submit</button>
  </form>
  <h1>Task:</h1>
  <ul>
    <li v-for = "(task,index) in tasks" :key="task">
      <span>{{ task }}</span>
      <button @click = "deleteTask(index)">x</button>
    </li>
  </ul>
  <a :href="link">google</a>
  <button @click="ToggleStatus">Change Status</button>
</template>
<style scoped>
  h1{
    color: red;
  }
</style>