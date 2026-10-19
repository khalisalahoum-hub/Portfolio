<script setup>
// ce que le parent me donne : mon prénom et mon nom
const props = defineProps({
  prenom: { type: String, required: true },
  nom: { type: String, required: true }
})

const nomComplet = computed(() => props.prenom + ' ' + props.nom)
const longueur = computed(() => nomComplet.value.length)
</script>

<template>
  <!-- mon nom, tapé dans un terminal -->
  <div class="titre-code">
    <p class="commande"><span class="invite">$</span> whoami</p>
    <h1 class="nom" :style="{ '--n': longueur }">{{ nomComplet }}</h1>
  </div>
</template>

<style scoped>
.commande {
  margin: 0 0 8px;
  color: var(--code-gris);
  font-family: var(--police-code);
  font-size: 0.95rem;
}

.invite {
  color: var(--code-vert);
}

/* mon nom : sa largeur vaut exactement le nombre de lettres (1ch = une lettre) */
.nom {
  display: block;
  width: calc(var(--n) * 1ch);
  margin: 0 auto 16px;
  padding-bottom: 0.05em;
  overflow: hidden;
  border-right: 0.1em solid var(--couleur-accent);
  font-family: var(--police-code);
  font-size: clamp(1.8rem, 7vw, 3.5rem);
  font-weight: 700;
  letter-spacing: 0;
  line-height: 1.2;
  white-space: nowrap;
  /* je tape lettre par lettre, et mon curseur clignote sans fin */
  animation:
    taper 1.6s steps(var(--n)) 0.5s backwards,
    curseur 1s step-end infinite;
}

/* je pars d'une largeur de 0 et j'arrive à la largeur normale */
@keyframes taper {
  from { width: 0; }
}

@keyframes curseur {
  50% { border-right-color: transparent; }
}

/* si la personne a demandé moins d'animations, tout est déjà écrit */
@media (prefers-reduced-motion: reduce) {
  .nom {
    animation: none;
  }
}
</style>