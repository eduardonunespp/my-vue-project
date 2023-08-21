<script>
import { ref, reactive, onMounted } from "vue";

export default {
  setup() {
    const email = ref("");
    const password = ref("");

    const user = reactive({
      email: email,
      password: password,
    });

    
    function login() {
        console.log(user.email, user.password);
    }

    const names = reactive([]);
    
    onMounted(() => {
      names.push(
        {
          firstName: "Sim",
          age: 10,
        },
        {
          firstName: "Sim",
          age: 10,
        },
        {
          firstName: "Sim",
          age: 10,
        }
        );
      });
      
      function remove(user){
        const index = names.findIndex(name => name.firstName === user.firstName)
        names.splice(index, 1)
      }
      
    return {
      user,
      login,
      names,
      remove
    };
  },
};
</script>

<template>
  <div>
    <h1>test</h1>

    <p v-if="user.email.length < 1">Email Vazio</p>
    <p v-else>Email Preechido</p>

    <ul v-if="names.length">
        <li v-for="name in names" :key="name.firstName" >{{ name.firstName }} - <button v-on:click="remove(name)">remove</button></li>
    </ul>
    <p v-else>Nenhum user encontrado</p>

    <form action="" @submit.prevent="login">
      <input type="text" placeholder="Email" v-model="user.email" />
      <input type="password" placeholder="Senha" v-model="user.password" />
      <button type="submit">Enviar</button>

      <p>Email: {{ user.email }}</p>
      <p>Senha: {{ user.password }}</p>
    </form>
  </div>
</template>
