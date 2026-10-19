<template>
  <!-- mon menu en haut de la page -->
  <nav class="menu">
    <NuxtLink to="/">Accueil</NuxtLink>
    <NuxtLink to="/parcours">Parcours</NuxtLink>
    <NuxtLink to="/cv">CV</NuxtLink>
  </nav>
</template>

<style scoped>
.menu {
  display: flex;
  gap: 24px;
  justify-content: center;
  padding: 16px;
}
</style>