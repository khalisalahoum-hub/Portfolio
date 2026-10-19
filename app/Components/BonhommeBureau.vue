<template>
  <!-- mon bonhomme qui code à son bureau, dessiné pixel par pixel -->
  <svg class="scene" viewBox="0 0 24 16" xmlns="http://www.w3.org/2000/svg" shape-rendering="crispEdges">
    <!-- le sol -->
    <rect x="0" y="15" width="24" height="1" fill="#cdbfa0" />

    <!-- ma chaise -->
    <rect x="5" y="5" width="1" height="6" fill="#555566" />

    <!-- mes jambes et mes chaussures -->
    <rect x="7" y="9" width="3" height="1" fill="#2b4a8a" />
    <rect x="8" y="10" width="2" height="4" fill="#2b4a8a" />
    <rect x="8" y="14" width="3" height="1" fill="#2b2b3a" />

    <!-- mon corps -->
    <rect class="chemise" x="7" y="5" width="3" height="4" />

    <!-- ma tête, mes cheveux et mon oeil -->
    <rect x="7" y="2" width="3" height="3" fill="#f2c9a0" />
    <rect x="7" y="1" width="3" height="1" fill="#3b2a1a" />
    <rect x="7" y="2" width="1" height="1" fill="#3b2a1a" />
    <rect x="9" y="3" width="1" height="1" fill="#2b2b3a" />

    <!-- le bureau et ses pieds -->
    <rect x="2" y="10" width="20" height="1" fill="#8b5a2b" />
    <rect x="3" y="11" width="1" height="4" fill="#8b5a2b" />
    <rect x="20" y="11" width="1" height="4" fill="#8b5a2b" />

    <!-- mon clavier -->
    <rect x="10" y="9" width="3" height="1" fill="#8d8d99" />

    <!-- mon écran -->
    <rect x="13" y="3" width="7" height="6" fill="#2b2b3a" />
    <rect x="16" y="9" width="2" height="1" fill="#2b2b3a" />
    <rect class="ecran" x="14" y="4" width="5" height="4" />

    <!-- les lignes de code sur l'écran -->
    <rect x="15" y="5" width="3" height="1" fill="white" />
    <rect x="15" y="6" width="2" height="1" fill="#5aa469" />
    <rect x="15" y="7" width="3" height="1" fill="white" />
    <rect class="curseur" x="17" y="6" width="1" height="1" fill="white" />

    <!-- mon bras et ma main qui tape -->
    <rect class="chemise" x="10" y="6" width="1" height="2" />
    <rect class="chemise" x="11" y="7" width="1" height="1" />
    <rect class="main-qui-tape" x="11" y="8" width="1" height="1" fill="#f2c9a0" />
  </svg>
</template>

<style scoped>
/* mon dessin garde des pixels nets quand il est agrandi */
.scene {
  display: block;
  width: 100%;
  max-width: 480px;
  margin: 0 auto;
  image-rendering: pixelated;
}

/* les couleurs viennent de ma palette */
.chemise {
  fill: var(--couleur-accent);
}

.ecran {
  fill: var(--couleur-bleu);
}

/* ma main monte et descend sur le clavier */
.main-qui-tape {
  animation: taper 0.4s steps(1) infinite;
}

/* mon curseur clignote */
.curseur {
  animation: clignoter 1s steps(1) infinite;
}

@keyframes taper {
  0% { transform: translateY(0); }
  50% { transform: translateY(1px); }
}

@keyframes clignoter {
  0% { opacity: 1; }
  50% { opacity: 0; }
}
</style>