<script setup>
// ce que le parent me donne : mes blocs de code, ma vitesse et mon décalage
const props = defineProps({
  blocs: { type: Array, required: true },
  nbLignesMax: { type: Number, default: 10 },
  vitesse: { type: Number, default: 70 },
  decalage: { type: Number, default: 0 }
})

const motsCles = ['const', 'let', 'function', 'return', 'async', 'await', 'for', 'of']

const numeroBloc = ref(0)
const nbCaracteres = ref(0)
let minuteur
let blocTermine = false

// le texte complet du bloc en cours, et la partie déjà tapée
const texteComplet = computed(() => props.blocs[numeroBloc.value].join('\n'))
const texteTape = computed(() => texteComplet.value.slice(0, nbCaracteres.value))

// je garde les dernières lignes : quand l'écran est plein, le code monte
const lignesVisibles = computed(() => {
  const lignes = texteTape.value.split('\n')
  return lignes.slice(-props.nbLignesMax)
})

// je découpe une ligne en morceaux pour les colorer
function colorer(ligne) {
  const morceaux = ligne.match(/\/\/.*|'[^']*'?|\w+|\s+|./g) || []
  return morceaux.map((texte) => {
    let classe = 'normal'
    if (texte.startsWith('//')) classe = 'commentaire'
    else if (texte.startsWith("'")) classe = 'chaine'
    else if (motsCles.includes(texte)) classe = 'mot'
    else if (/^\d+$/.test(texte)) classe = 'nombre'
    return { texte, classe }
  })
}

// j'ajoute une lettre, puis je programme la suivante
function avancer() {
  const total = texteComplet.value.length
  let attente = props.vitesse + Math.random() * 60

  if (nbCaracteres.value < total) {
    nbCaracteres.value++
    // petite pause en fin de ligne, comme quelqu'un qui réfléchit
    if (texteComplet.value[nbCaracteres.value - 1] === '\n') attente += 250
  } else if (!blocTermine) {
    // le bloc est fini : je laisse le temps de le lire
    blocTermine = true
    attente = 3500
  } else {
    // je passe au bloc suivant
    blocTermine = false
    numeroBloc.value = (numeroBloc.value + 1) % props.blocs.length
    nbCaracteres.value = 0
    attente = 600
  }

  minuteur = setTimeout(avancer, attente)
}

onMounted(() => {
  // si la personne a demandé moins d'animations, j'affiche le code d'un coup
  if (window.matchMedia('(prefers-reduced-motion: reduce)').matches) {
    nbCaracteres.value = texteComplet.value.length
    return
  }
  minuteur = setTimeout(avancer, props.decalage)
})

// j'arrête tout quand je quitte la page
onUnmounted(() => {
  clearTimeout(minuteur)
})
</script>

<template>
  <!-- un écran qui tape du code tout seul -->
  <div class="ecran">
    <div v-for="(ligne, i) in lignesVisibles" :key="i" class="ligne">
      <span v-for="(morceau, j) in colorer(ligne)" :key="j" :class="morceau.classe">{{ morceau.texte }}</span>
      <span v-if="i === lignesVisibles.length - 1" class="curseur"></span>
    </div>
  </div>
</template>

<style scoped>
/* mon écran cache l'ancien code de l'image */
.ecran {
  box-sizing: border-box;
  padding: 0.4cqw 0.5cqw;
  overflow: hidden;
  background-color: #0b1630;
  text-align: left;
}

/* une ligne de code, sa hauteur est fixe pour que les lignes vides comptent */
.ligne {
  height: 0.78cqw;
  font-family: 'Courier New', monospace;
  font-size: 0.6cqw;
  line-height: 0.78cqw;
  white-space: pre;
}

/* mes couleurs de code, discrètes */
.mot { color: #9a7bc8; }
.chaine { color: #7fb085; }
.nombre { color: #c99a6b; }
.commentaire { color: #566078; }
.normal { color: #9fb0cc; }

/* mon curseur clignote */
.curseur {
  display: inline-block;
  width: 0.3cqw;
  height: 0.55cqw;
  vertical-align: middle;
  background-color: #d8e2f5;
  animation: clignoter 1s steps(1) infinite;
}

@keyframes clignoter {
  0% { opacity: 1; }
  50% { opacity: 0; }
}
</style>