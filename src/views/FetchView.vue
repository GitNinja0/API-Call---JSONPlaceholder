<script>
import {ref} from 'vue';

export default{
  setup() {
    const users = ref([])

    fetch('https://jsonplaceholder.typicode.com/users')
      .then(response => response.json())
      .then(data => {
        console.log(data)
        users.value = data.slice(0, 10).map(user => ({
          id: user.id,
          name: user.name,
          city: user.address.city
        }))
      })
      return {users}
  }

}

</script>
<template>
    <div class="about">
        <h1>Tareaaaa</h1>
    </div>
  <div v-for="user in users">
    <div class="div1">
      <h1>{{ user.id }}</h1>
      <h1>{{ user.name }}</h1>
      <h1>{{ user.city }}</h1>
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
  
}
</style>
