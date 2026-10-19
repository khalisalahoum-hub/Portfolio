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
    <h1>Mon parcours</h1>
    <p class="intro">Ce que j'ai fait, et ce qui arrive.</p>

    <!-- ma frise : une ligne au milieu, des cartes de chaque côté -->
    <ol class="frise">
      <li
        v-for="(etape, i) in etapes"
        :key="etape.titre"
        class="etape"
        :class="[i % 2 === 0 ? 'gauche' : 'droite', etape.statut]"
      >
        <div class="carte">
          <span class="annee">{{ etape.annee }}</span>
          <h2>{{ etape.titre }}</h2>
          <p>{{ etape.description }}</p>
          <span v-if="etape.statut === 'futur'" class="badge">À venir</span>
        </div>
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
  margin: 0 0 64px;
  color: var(--couleur-texte-doux);
}

/* ma frise */
.frise {
  position: relative;
  margin: 0;
  padding: 0;
  list-style: none;
}

/* ma ligne verticale au milieu */
.frise::before {
  content: '';
  position: absolute;
  top: 0;
  bottom: 0;
  left: 50%;
  width: 2px;
  background-color: var(--couleur-bordure);
  transform: translateX(-50%);
}

/* chaque étape occupe une moitié de la largeur */
.etape {
  position: relative;
  width: 50%;
  padding-bottom: 48px;
}

.etape.gauche {
  padding-right: 40px;
}

.etape.droite {
  margin-left: 50%;
  padding-left: 40px;
}

/* mon point sur la ligne */
.etape::before {
  content: '';
  position: absolute;
  top: 24px;
  width: 14px;
  height: 14px;
  border: 3px solid var(--couleur-fond);
  border-radius: 50%;
  background-color: var(--couleur-accent);
}

.etape.gauche::before {
  right: -7px;
}

.etape.droite::before {
  left: -7px;
}

/* les étapes à venir : point creux et carte en pointillés */
.etape.futur::before {
  border-color: var(--couleur-accent);
  background-color: var(--couleur-fond);
}

.carte {
  padding: 24px;
  border: 1px solid var(--couleur-bordure);
  border-radius: 12px;
  background-color: var(--couleur-surface);
}

.etape.futur .carte {
  border-style: dashed;
}

.annee {
  color: var(--couleur-accent);
  font-size: 0.85rem;
  font-weight: 600;
  letter-spacing: 0.1em;
}

.carte h2 {
  margin: 4px 0 8px;
  font-size: 1.25rem;
}

.carte p {
  margin: 0;
  color: var(--couleur-texte-doux);
}

.badge {
  display: inline-block;
  margin-top: 12px;
  padding: 2px 10px;
  border: 1px solid var(--couleur-bleu);
  border-radius: 999px;
  color: var(--couleur-bleu);
  font-size: 0.75rem;
}

/* sur téléphone : la ligne passe à gauche et toutes les cartes sont du même côté */
@media (max-width: 700px) {
  .frise::before {
    left: 7px;
  }

  .etape,
  .etape.gauche,
  .etape.droite {
    width: 100%;
    margin-left: 0;
    padding-left: 40px;
    padding-right: 0;
  }

  .etape.gauche::before,
  .etape.droite::before {
    left: 0;
    right: auto;
  }
}
</style>