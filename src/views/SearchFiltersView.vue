<script>
import {ref, computed} from 'vue';

export default{
  setup() {
    const users = ref([])
    const searchByID = ref('')

    fetch('https://jsonplaceholder.typicode.com/users')
      .then(response => response.json())
      .then(data => {
        console.log(data)
        users.value = data.slice(0, 10).map(user => ({
          id: user.id,
          name: user.name,
          city: user.address.city,
          phone: user.phone
        }))
      })
      const filteredUsers = computed(() =>{
        if(!searchByID.value){
          return users.value
        }
        return users.value.filter(user => user.id === parseInt(searchByID.value))
      })

      return {filteredUsers, searchByID}
  }

}

</script>
<template>
  <div class="about">
        <input type="text" v-model="searchByID">
  </div>
  <div v-for="user in filteredUsers" :key="user.id">
    <div class="div1">
      <h1>{{ user.id }}</h1>
      <h1>{{ user.name }}</h1>
      <h1>{{ user.city }}</h1>
      <h1>{{ user.phone }}</h1>
    </div>
  </div>

</template>
<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
.div1{
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
  margin-bottom: 2rem;
  
}</style>