<template>
  <main>
    <!-- mon décor : la scène prend toute la largeur -->
    <section>
      <SceneBureau />
    </section>

    <!-- ma présentation remonte sur le bas de l'image -->
    <section class="presentation">
      <p class="etiquette">Portfolio</p>
      <h1>Khalis</h1>
      <p class="titre">Apprenti ingénieur en informatique</p>
      <p class="description">
        Je me forme au développement web avec Nuxt et Vue.
      </p>

      <div class="boutons">
        <NuxtLink class="bouton" to="/parcours">Voir mon parcours</NuxtLink>
        <NuxtLink class="bouton bouton-secondaire" to="/cv">Mon CV</NuxtLink>
      </div>
    </section>
  </main>
</template>

<style scoped>
.presentation {
  position: relative;
  max-width: 720px;
  margin: -6% auto 0;
  padding: 0 24px 80px;
  text-align: center;
}

.etiquette {
  margin: 0 0 8px;
  color: var(--couleur-accent);
  font-size: 0.85rem;
  font-weight: 600;
  letter-spacing: 0.15em;
  text-transform: uppercase;
}

h1 {
  margin: 0 0 8px;
  font-size: clamp(2.5rem, 6vw, 4rem);
}

.titre {
  margin: 0 0 16px;
  font-size: 1.25rem;
  color: var(--couleur-texte-doux);
}

.description {
  margin: 0 0 32px;
  color: var(--couleur-texte-doux);
}

.boutons {
  display: flex;
  gap: 16px;
  justify-content: center;
  flex-wrap: wrap;
}
</style>