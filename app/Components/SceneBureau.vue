<script setup>
// mes blocs de code : chaque bloc est une liste de lignes
const blocsGauche = [
  ['serveur/', '  routes/', '    users.js', '    data.js', '  index.js', 'package.json'],
  ['client/', '  src/', '    App.jsx', '    api.js', '  index.html', 'vite.config.js']
]

const blocsCentre = [
  [
    'const app = express();',
    'app.use(express.json());',
    '',
    "app.get('/', (req, res) => {",
    '  const data = getData();',
    '  res.json({ ok: true });',
    '});',
    '',
    'app.listen(3000, () => {',
    "  console.log('Server ready');",
    '});'
  ],
  [
    'function somme(liste) {',
    '  let total = 0;',
    '  for (const n of liste) {',
    '    total += n;',
    '  }',
    '  return total;',
    '}',
    '',
    'console.log(somme([1, 2, 3]));'
  ]
]

const blocsDroite = [
  [
    'function fetchData() {',
    "  return fetch('/api/data')",
    '    .then(res => res.json())',
    '    .then(data => data);',
    '}'
  ],
  [
    'useEffect(() => {',
    '  fetchData().then(setData);',
    '}, []);',
    '',
    'const total = data.length;',
    'console.log(total);'
  ],
  [
    '.carte {',
    '  display: flex;',
    '  gap: 10px;',
    '  color: #fff;',
    '}'
  ]
]
</script>

<template>
  <!-- mon bureau la nuit, avec du code qui s'écrit sur mes trois écrans -->
  <div class="scene">
    <img class="fond" src="/bureau-nuit.png" alt="Mon bureau la nuit en pixel art" />

    <!-- mon dégradé qui fond les bords de l'image dans le fond du site -->
    <div class="fondu"></div>

    <EcranCode class="ecran-gauche" :blocs="blocsGauche" :vitesse="90" :decalage="1800" />
    <EcranCode class="ecran-centre" :blocs="blocsCentre" :vitesse="65" :decalage="0" />
    <EcranCode class="ecran-droite" :blocs="blocsDroite" :vitesse="75" :decalage="900" />
  </div>
</template>

<style scoped>
/* ma scène garde le format de l'image et sert de référence pour les tailles */
.scene {
  position: relative;
  width: 100%;
  max-width: 1400px;
  margin: 0 auto;
  aspect-ratio: 1585 / 992;
  container-type: inline-size;
}

.fond {
  display: block;
  width: 100%;
  height: 100%;
  image-rendering: pixelated;
}

/* deux dégradés superposés : les côtés et le bas se fondent dans le fond du site */
.fondu {
  position: absolute;
  inset: 0;
  pointer-events: none;
  background:
    linear-gradient(to right, var(--couleur-fond) 0%, transparent 10%, transparent 90%, var(--couleur-fond) 100%),
    linear-gradient(to bottom, transparent 55%, var(--couleur-fond) 100%);
}

/* mes trois écrans sont posés par-dessus l'image */
.ecran-gauche,
.ecran-centre,
.ecran-droite {
  position: absolute;
}

/* l'écran de gauche est un peu incliné sur l'image */
.ecran-gauche {
  left: 14.2%;
  top: 38.5%;
  width: 8.6%;
  height: 16.5%;
  transform: skewY(-4deg);
}

/* l'écran du milieu s'arrête avant la tête du personnage */
.ecran-centre {
  left: 29.3%;
  top: 32.9%;
  width: 12.6%;
  height: 20.2%;
}

.ecran-droite {
  left: 53.2%;
  top: 35%;
  width: 14.8%;
  height: 19%;
}
</style>