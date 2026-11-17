<script setup>
// mes étapes : celles que j'ai faites et celles qui arrivent
const etapes = ref([
  {
    annee: 2025,
    titre: 'Intégration au CESI Nanterre',
    description: "Début de mes études d'ingénieur en informatique.",
    statut: 'passe'
  },
  {
    annee: 2026,
    titre: 'Deuxième année de prépa intégrée',
    description: "Je consolide mes bases en maths et en informatique.",
    statut: 'passe'
  },
  {
    annee: 2026,
    titre: 'Mon premier projet web',
    description: 'Ce portfolio, construit avec Nuxt, Vue et Git.',
    statut: 'passe'
  },
  {
    annee: 2027,
    titre: 'Cycle ingénieur',
    description: "Je choisis ma spécialité et je pars en alternance.",
    statut: 'futur'
  },
  {
    annee: 2029,
    titre: "Diplôme d'ingénieur",
    description: 'Objectif : un poste de développeur full-stack.',
    statut: 'futur'
  }
])
</script>

<template>
  <main class="conteneur page">
    <p class="etiquette">parcours</p>
    <h1>Mon parcours</h1>
    <p class="intro">Ce que j'ai fait, et ce qui arrive.</p>

    <!-- mon historique, présenté comme un git log -->
    <ol class="historique">
      <li
        v-for="etape in etapes"
        :key="etape.titre"
        class="etape"
        :class="etape.statut"
      >
        <span class="noeud"></span>
        <p class="annee">{{ etape.annee }}</p>
        <h2>
          {{ etape.titre }}
          <span v-if="etape.statut === 'futur'" class="branche">à venir</span>
        </h2>
        <p class="description">{{ etape.description }}</p>
      </li>
    </ol>
  </main>
</template>

<style scoped>
.page {
  padding-top: 64px;
  padding-bottom: 96px;
}

h1 {
  margin: 0 0 8px;
  font-size: clamp(2rem, 5vw, 3rem);
}

.intro {
  margin: 0 0 56px;
  color: var(--couleur-texte-doux);
}

/* mon historique : une ligne verticale à gauche */
.historique {
  position: relative;
  margin: 0;
  padding: 0;
  list-style: none;
}

.historique::before {
  content: '';
  position: absolute;
  top: 8px;
  bottom: 8px;
  left: 7px;
  width: 2px;
  background-color: var(--couleur-bordure);
}

.etape {
  position: relative;
  padding: 0 0 40px 40px;
}

/* mon point sur la ligne : plein pour le passé, creux pour le futur */
.noeud {
  position: absolute;
  top: 4px;
  left: 0;
  width: 16px;
  height: 16px;
  border: 2px solid var(--code-vert);
  border-radius: 50%;
  background-color: var(--couleur-fond);
}

.etape.passe .noeud {
  background-color: var(--code-vert);
}

.etape.futur .noeud {
  border-color: var(--code-orange);
}

.annee {
  margin: 0 0 4px;
  color: var(--code-gris);
  font-family: var(--police-code);
  font-size: 0.85rem;
}

.etape h2 {
  margin: 0 0 6px;
  font-size: 1.25rem;
}

/* mon étiquette "à venir", comme le nom d'une branche */
.branche {
  margin-left: 8px;
  padding: 2px 8px;
  border: 1px solid var(--code-orange);
  border-radius: 4px;
  color: var(--code-orange);
  font-family: var(--police-code);
  font-size: 0.75rem;
  font-weight: 400;
  vertical-align: middle;
}

.description {
  margin: 0;
  color: var(--couleur-texte-doux);
}
</style>