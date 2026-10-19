<template>
  <!-- mon menu en haut de la page -->
  <header class="entete">
    <nav class="menu">
      <NuxtLink class="logo" to="/">Khalis</NuxtLink>

      <div class="liens">
        <NuxtLink to="/">Accueil</NuxtLink>
        <NuxtLink to="/parcours">Parcours</NuxtLink>
      </div>
    </nav>
  </header>
</template>

<style scoped>
/* mon menu reste collé en haut, avec un fond légèrement flouté */
.entete {
  position: sticky;
  top: 0;
  z-index: 10;
  background-color: rgba(10, 17, 40, 0.8);
  backdrop-filter: blur(12px);
  border-bottom: 1px solid var(--couleur-bordure);
}

.menu {
  display: flex;
  align-items: center;
  justify-content: space-between;
  max-width: 1100px;
  margin: 0 auto;
  padding: 16px 24px;
}

.logo {
  font-weight: 700;
  font-size: 1.1rem;
  text-decoration: none;
}

.liens {
  display: flex;
  gap: 24px;
}

.liens a {
  padding: 4px 0;
  border-bottom: 2px solid transparent;
  color: var(--couleur-texte-doux);
  text-decoration: none;
  transition: color 0.15s;
}

.liens a:hover {
  color: var(--couleur-texte);
}

/* le lien de la page où je me trouve */
.liens a.router-link-exact-active {
  border-bottom-color: var(--couleur-accent);
  color: var(--couleur-texte);
}
</style>