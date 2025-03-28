<script>
  export default{
    data(){
      return {
        name: 'Jonh',
        status: true,
        status1: 'active',
        tasks: ['test1','test2'],
        link: 'https://chatgpt.com/c/67ea0af1-3cdc-800f-a52d-d4e8233f5d90',
      }
    },
    methods: {
      ToggleStatus(){
        if(this.status1 === 'active' ){
          this.status1 = 'pedding';
        }else if(this.status1 === 'pedding'){
          this.status1 = 'inactive';
        }else{
          this.status1 = 'active';
        }
      },
    },
  }
</script>
<template>
  <h1>{{ name }}</h1>
  <p v-if="status">true</p>
  <p v-else>not</p>
  <p v-if="status1 === 'active'">active</p>
  <p v-if="status1 === 'pedding'">pedding</p>
  <h1>Task:</h1>
  <ul>
    <li v-for = "task in tasks" :key="task">
      {{ task }}
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