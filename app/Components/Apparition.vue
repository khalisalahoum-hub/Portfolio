<script setup>
// ce composant dit à son contenu quand il est visible à l'écran
const boite = ref(null)
const visible = ref(false)
let observateur = null

onMounted(() => {
  // si la personne a demandé moins d'animations, tout est visible tout de suite
  if (window.matchMedia('(prefers-reduced-motion: reduce)').matches) {
    visible.value = true
    return
  }

  // l'observateur nous prévient quand la boîte entre dans l'écran
  observateur = new IntersectionObserver(
    (entrees) => {
      if (entrees[0].isIntersecting) {
        visible.value = true
        // une fois visible, on n'a plus besoin de surveiller
        observateur.disconnect()
      }
    },
    { threshold: 0.15 }
  )

  observateur.observe(boite.value)
})

// j'arrête de surveiller quand je quitte la page
onUnmounted(() => {
  if (observateur) observateur.disconnect()
})
</script>

<template>
  <!-- je donne "visible" au contenu : il est faux au début, puis vrai quand on arrive dessus -->
  <div ref="boite">
    <slot :visible="visible" />
  </div>
</template>