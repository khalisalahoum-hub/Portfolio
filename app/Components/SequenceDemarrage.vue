<script setup>
// les lignes de mon démarrage : elles parlent de ce que je sais faire
const lignes = [
  { etat: 'OK', texte: 'chargement du noyau' },
  { etat: 'OK', texte: 'initialisation des capteurs' },
  { etat: 'OK', texte: 'configuration du réseau (VLAN 10, 20, 30)' },
  { etat: 'OK', texte: 'compilation des projets en C' },
  { etat: 'OK', texte: 'lecture du CV' },
  { etat: 'OK', texte: 'connexion établie' }
]

// la séquence est affichée dès le départ, puis cachée si je l'ai déjà vue
const visible = ref(true)
const sortie = ref(false)
const nbLignes = ref(0)

// le pourcentage dépend du nombre de lignes déjà affichées
const progression = computed(() => Math.round((nbLignes.value / lignes.length) * 100))

let minuteur
let minuteurFin

// je fais disparaître la séquence en fondu, puis je la retire de la page
function terminer() {
  if (sortie.value) return
  sortie.value = true
  clearInterval(minuteur)
  clearTimeout(minuteurFin)
  document.body.style.overflow = ''

  // je retiens que je l'ai vue, pour ne pas la rejouer à chaque page
  try {
    sessionStorage.setItem('demarrage-vu', 'oui')
  } catch (erreur) {
    // le stockage peut être bloqué : ce n'est pas grave
  }

  setTimeout(() => {
    visible.value = false
  }, 600)
}

// Entrée, Espace ou Échap passent la séquence
function surTouche(evenement) {
  if (['Enter', ' ', 'Escape'].includes(evenement.key)) terminer()
}

onMounted(() => {
  let dejaVu = false
  try {
    dejaVu = sessionStorage.getItem('demarrage-vu') === 'oui'
  } catch (erreur) {
    dejaVu = false
  }

  // si je l'ai déjà vue, ou si la personne veut moins d'animations, je saute tout
  const moinsAnimations = window.matchMedia('(prefers-reduced-motion: reduce)').matches
  if (dejaVu || moinsAnimations) {
    visible.value = false
    return
  }

  // pendant la séquence, la page derrière ne défile pas
  document.body.style.overflow = 'hidden'
  window.addEventListener('keydown', surTouche)

  // j'affiche une nouvelle ligne toutes les 380 ms
  minuteur = setInterval(() => {
    if (nbLignes.value < lignes.length) {
      nbLignes.value++
    } else {
      // tout est affiché : je laisse une courte pause, puis je termine
      clearInterval(minuteur)
      minuteurFin = setTimeout(terminer, 700)
    }
  }, 380)
})

// je nettoie tout quand je quitte la page
onUnmounted(() => {
  clearInterval(minuteur)
  clearTimeout(minuteurFin)
  window.removeEventListener('keydown', surTouche)
  document.body.style.overflow = ''
})
</script>

<template>
  <!-- mon démarrage : un écran noir par-dessus le site, avec des lignes de journal -->
  <div v-if="visible" class="demarrage" :class="{ sortie }" role="status" aria-live="polite">
    <div class="terminal">
      <p class="entete">khalis-os v1.0 / démarrage</p>

      <p v-for="(ligne, i) in lignes.slice(0, nbLignes)" :key="i" class="ligne">
        <span class="etat">[ {{ ligne.etat }} ]</span> {{ ligne.texte }}
      </p>

      <div class="barre">
        <div class="remplissage" :style="{ width: progression + '%' }"></div>
      </div>
      <p class="pourcentage">{{ progression }} %</p>
    </div>

    <button class="passer" type="button" @click="terminer">passer →</button>
  </div>
</template>

<style scoped>
/* mon écran de démarrage recouvre toute la page */
.demarrage {
  position: fixed;
  inset: 0;
  z-index: 100;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 24px;
  background-color: var(--couleur-fond);
  transition: opacity 0.6s ease;
}

/* au moment de partir, je deviens transparent */
.demarrage.sortie {
  opacity: 0;
  pointer-events: none;
}

.terminal {
  width: 100%;
  max-width: 520px;
  font-family: var(--police-code);
  font-size: 0.9rem;
}

.entete {
  margin: 0 0 20px;
  color: var(--code-gris);
}

.ligne {
  margin: 0 0 6px;
  color: var(--couleur-texte-doux);
}

.etat {
  color: var(--code-vert);
}

/* ma barre de progression */
.barre {
  height: 6px;
  margin-top: 24px;
  border-radius: 3px;
  background-color: var(--couleur-bordure);
  overflow: hidden;
}

.remplissage {
  height: 100%;
  background-color: var(--couleur-accent);
  transition: width 0.3s ease;
}

.pourcentage {
  margin: 8px 0 0;
  color: var(--couleur-accent);
  text-align: right;
}

.passer {
  position: absolute;
  right: 24px;
  bottom: 24px;
  padding: 8px 14px;
  border: 1px solid var(--couleur-bordure);
  border-radius: 6px;
  background: transparent;
  color: var(--couleur-texte-doux);
  font-family: var(--police-code);
  font-size: 0.8rem;
  cursor: pointer;
}

.passer:hover {
  border-color: var(--couleur-texte-doux);
  color: var(--couleur-texte);
}
</style>