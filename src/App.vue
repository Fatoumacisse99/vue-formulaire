<template>
  <div id="app">
    <header>
      <h1>Application de Formulaire Utilisateur</h1>
    </header>
    
    <!-- Composant du Formulaire de Saisie -->
    <UserForm />
  </div>
</template>

<script>
// Importation du composant UserForm
import UserForm from './components/UserForm.vue';

export default {
  name: 'App',
  components: {
    UserForm
  }
};
</script>

<style scoped>
#app {
  font-family: 'Arial', sans-serif;
  text-align: center;
  color: #333;
  margin-top: 20px;
}

header {
  margin-bottom: 20px;
}

header h1 {
  font-size: 32px;
  color: #343a40;
  margin-bottom: 10px;
}
</style>
