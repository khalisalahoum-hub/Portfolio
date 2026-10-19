<script setup>
// les technologies que j'apprends
const technologies = ['HTML', 'CSS', 'JavaScript', 'Vue', 'Nuxt', 'Node.js', 'Git', 'GitHub']

// je les affiche deux fois pour que le défilement ne s'arrête jamais
const technologiesDoublees = [...technologies, ...technologies]
</script>

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
        <!-- un fichier se télécharge avec une balise a, pas avec NuxtLink -->
        <a class="bouton bouton-secondaire" href="/Cv_Khalis_Alahoum_.pdf" download>Télécharger mon CV</a>
      </div>
    </section>

    <!-- mon bandeau de technologies qui défile en boucle -->
    <section class="bandeau" aria-label="Technologies que j'apprends">
      <div class="defilement">
        <span v-for="(techno, i) in technologiesDoublees" :key="i" class="techno">{{ techno }}</span>
      </div>
    </section>

    <!-- ma présentation en quelques lignes -->
    <section class="conteneur a-propos">
      <p class="etiquette">À propos</p>
      <h2>Qui suis-je ?</h2>
      <p>
        Je suis étudiant en cycle préparatoire intégré au CESI Nanterre.
        J'apprends à créer des sites web, et ce portfolio est mon premier projet complet.
      </p>
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

/* mon bandeau de technologies */
.bandeau {
  overflow: hidden;
  border-top: 1px solid var(--couleur-bordure);
  border-bottom: 1px solid var(--couleur-bordure);
}

.defilement {
  display: flex;
  width: max-content;
  animation: defiler 30s linear infinite;
}

.techno {
  padding: 20px 32px;
  color: var(--couleur-texte-doux);
  font-weight: 600;
  white-space: nowrap;
}

/* la liste est affichée deux fois : je monte d'une moitié, puis je recommence */
@keyframes defiler {
  from { transform: translateX(0); }
  to { transform: translateX(-50%); }
}

/* si la personne a demandé moins d'animations, je coupe */
@media (prefers-reduced-motion: reduce) {
  .defilement { animation: none; }
}

.a-propos {
  max-width: 720px;
  padding-top: 96px;
  padding-bottom: 96px;
}

.a-propos h2 {
  margin: 0 0 16px;
  font-size: 2rem;
}

.a-propos p:last-child {
  color: var(--couleur-texte-doux);
}
</style>