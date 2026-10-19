<script setup>
// le lien de mon CV : le nom doit être exactement celui du fichier dans le dossier public
const lienCv = '/CV_Khalis_Alahoum_.pdf'

// mes compétences, rangées par famille
const groupesCompetences = [
  { titre: 'Programmation', liste: ['C', 'Python'] },
  { titre: 'Embarqué et réseau', liste: ['Arduino', 'Microcontrôleurs', 'Linux', 'Cisco Packet Tracer', 'VLAN', 'TCP/IP'] },
  { titre: 'Données et outils', liste: ['Bases de données', 'Git', 'GitHub', 'Excel', 'Word', 'PowerPoint'] },
  { titre: 'Web (en apprentissage)', liste: ['HTML', 'CSS', 'JavaScript', 'Vue', 'Nuxt', 'Node.js'] }
]

// mes projets d'école d'ingénieur : "fichier" est le nom affiché dans la fenêtre
const projets = [
  {
    fichier: 'station_meteo.c',
    titre: 'Station météo embarquée',
    resume: "Avec mon équipe, j'ai conçu un prototype de station météo. J'ai programmé en C la lecture des capteurs, les entrées/sorties et les interruptions sur des microcontrôleurs, et j'ai pris en main un système Linux.",
    tags: ['C', 'Microcontrôleurs', 'Linux', 'Travail en équipe']
  },
  {
    fichier: 'digicode.ino',
    titre: 'Digicode sécurisé',
    resume: "J'ai conçu et programmé en C un digicode sur carte Arduino avec plusieurs niveaux d'accès. J'ai aussi testé et corrigé le code embarqué.",
    tags: ['C', 'Arduino', 'Sécurité']
  },
  {
    fichier: 'base_de_donnees.sql',
    titre: 'Base de données sécurisée',
    resume: "J'ai modélisé et créé une base de données complète, avec un accès administrateur, la gestion des droits d'utilisation et des requêtes ciblées.",
    tags: ['Bases de données', 'Requêtes', "Droits d'accès"]
  },
  {
    fichier: 'reseau.pkt',
    titre: 'Infrastructure réseau',
    resume: "J'ai conçu et simulé un réseau complet sous Cisco Packet Tracer : plan d'adressage IP, sous-réseaux, VLAN, routage entre les sous-réseaux, TCP/IP et DHCP.",
    tags: ['Cisco Packet Tracer', 'VLAN', 'TCP/IP', 'DHCP']
  }
]

// quelques faits sur moi
const faits = [
  { titre: 'formation', texte: "CESI, cycle ingénieur, 2e année de prépa intégrée. Avant : bac scientifique, option mathématiques, informatique et ingénierie." },
  { titre: 'langues', texte: 'Français (natif), anglais (B2), espagnol.' },
  { titre: 'qualités', texte: 'Sociable, perfectionniste, ponctuel et autonome.' },
  { titre: 'loisirs', texte: 'Basket, automobile, photographie, voyage et musique.' }
]

// mon expérience professionnelle
const missions = [
  'Accueil et conseil des clients sur les expériences de réalité virtuelle.',
  'Diagnostic et réparation des problèmes techniques sur les PC et les casques.',
  "Installation, paramétrage et entretien des équipements.",
  "Participation à l'organisation d'événements et d'activités promotionnelles."
]
</script>

<template>
  <main>
    <!-- mon accueil : une grille discrète en fond, et mon nom tapé dans un terminal -->
    <section class="hero">
      <div class="presentation">
        <p class="etiquette">portfolio</p>
        <TitreCode prenom="Khalis" nom="Alahoum" />
        <p class="titre apres">Étudiant en cycle ingénieur en informatique</p>
        <p class="description apres">
          Je programme en C et en Python, et je découvre le développement web avec Nuxt et Vue.
        </p>
        <p class="statut apres apres-2">
          <span class="point"></span>Stage recherché du 5 avril au 2 juillet
        </p>

        <div class="boutons apres apres-3">
          <NuxtLink class="bouton" to="/parcours">Voir mon parcours</NuxtLink>
          <!-- un fichier se télécharge avec une balise a, pas avec NuxtLink -->
          <a class="bouton bouton-secondaire" :href="lienCv" download>Télécharger mon CV</a>
        </div>
      </div>
    </section>

    <!-- qui je suis -->
    <Apparition v-slot="{ visible }">
      <section class="conteneur bloc revele" :class="{ visible }">
        <p class="etiquette">à propos</p>
        <h2>Qui suis-je ?</h2>
        <p class="texte">
          Je suis étudiant en cycle ingénieur au CESI Nanterre, en 2e année de prépa intégrée.
          J'aime programmer, surtout en C, et les projets qui mélangent le code et l'électronique.
          J'apprends aussi le web : ce portfolio est mon premier projet complet.
        </p>
        <p class="texte">
          Je cherche un stage de 8 à 12 semaines, du 5 avril au 2 juillet, en ingénierie informatique.
        </p>

        <div class="faits">
          <div v-for="fait in faits" :key="fait.titre" class="fait">
            <h3>{{ fait.titre }}</h3>
            <p>{{ fait.texte }}</p>
          </div>
        </div>
      </section>
    </Apparition>

    <!-- mes compétences : les pastilles apparaissent l'une après l'autre -->
    <Apparition v-slot="{ visible }">
      <section class="conteneur bloc" :class="{ visible }">
        <p class="etiquette">compétences</p>
        <h2>Ce que je sais faire</h2>
        <p class="texte">Ce que j'ai appris en cours, en projet et en auto-apprentissage.</p>

        <div v-for="groupe in groupesCompetences" :key="groupe.titre" class="groupe">
          <h3>{{ groupe.titre }}</h3>
          <div class="chips">
            <span
              v-for="(competence, i) in groupe.liste"
              :key="competence"
              class="chip"
              :style="{ '--i': i }"
            >{{ competence }}</span>
          </div>
        </div>
      </section>
    </Apparition>

    <!-- mes projets : chaque projet est une fenêtre d'éditeur -->
    <Apparition v-slot="{ visible }">
      <section class="conteneur bloc" :class="{ visible }">
        <p class="etiquette">projets</p>
        <h2>Mes projets</h2>
        <p class="texte">Quatre projets réalisés pendant ma formation au CESI.</p>

        <div class="projets">
          <FenetreCode
            v-for="(projet, i) in projets"
            :key="projet.titre"
            :fichier="projet.fichier"
            class="carte-projet"
            :style="{ '--i': i }"
          >
            <p class="ecole">projet d'école d'ingénieur</p>
            <h3>{{ projet.titre }}</h3>
            <p class="resume">{{ projet.resume }}</p>
            <div class="tags">
              <span v-for="tag in projet.tags" :key="tag" class="tag">{{ tag }}</span>
            </div>
          </FenetreCode>
        </div>
      </section>
    </Apparition>

    <!-- mon expérience -->
    <Apparition v-slot="{ visible }">
      <section class="conteneur bloc revele" :class="{ visible }">
        <p class="etiquette">expérience</p>
        <h2>Mon expérience</h2>

        <FenetreCode fichier="zero-latency.md" class="carte-experience">
          <p class="badge"><span class="point"></span>en cours</p>
          <h3>Vendeur technicien et équipier polyvalent</h3>
          <p class="entreprise">Zero Latency, Cormeilles-en-Parisis. Octobre 2025 à mars 2027.</p>
          <ul>
            <li v-for="mission in missions" :key="mission">{{ mission }}</li>
          </ul>
        </FenetreCode>
      </section>
    </Apparition>

    <!-- mon contact -->
    <Apparition v-slot="{ visible }">
      <section class="conteneur bloc contact revele" :class="{ visible }">
        <p class="etiquette">contact</p>
        <h2>Me contacter</h2>
        <p class="texte">
          Une question, une proposition de stage ? Écrivez-moi, je répondrai avec plaisir.
        </p>

        <div class="boutons">
          <a class="bouton" href="mailto:khalisalahoum@gmail.com">M'écrire un mail</a>
          <a class="bouton bouton-secondaire" :href="lienCv" download>Télécharger mon CV</a>
        </div>
        <p class="lieu">Paris, région parisienne</p>
      </section>
    </Apparition>

    <!-- mon décor pixel art, tout en bas de la page -->
    <section>
      <SceneBureau />
    </section>
  </main>
</template>

<style scoped>
/* ----- mon accueil ----- */
.hero {
  position: relative;
  overflow: hidden;
}

/* une grille de points discrète, comme dans un éditeur, qui s'efface vers le bas */
.hero::before {
  content: '';
  position: absolute;
  inset: 0;
  pointer-events: none;
  background-image: radial-gradient(var(--couleur-bordure) 1px, transparent 1px);
  background-size: 28px 28px;
  -webkit-mask-image: linear-gradient(to bottom, black 30%, transparent 100%);
  mask-image: linear-gradient(to bottom, black 30%, transparent 100%);
}

.presentation {
  position: relative;
  max-width: 720px;
  margin: 0 auto;
  padding: 96px 24px 80px;
  text-align: center;
}

.titre {
  margin: 0 0 16px;
  font-size: 1.25rem;
  color: var(--couleur-texte-doux);
}

.description {
  margin: 0 0 24px;
  color: var(--couleur-texte-doux);
}

/* ma disponibilité pour le stage */
.statut {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  margin: 0 0 32px;
  padding: 6px 14px;
  border: 1px solid var(--couleur-bordure);
  border-radius: 6px;
  background-color: var(--couleur-surface);
  color: var(--couleur-texte-doux);
  font-family: var(--police-code);
  font-size: 0.8rem;
}

/* mon petit voyant vert, qui pulse doucement */
.point {
  display: inline-block;
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background-color: var(--code-vert);
  animation: pulser 2s ease-in-out infinite;
}

@keyframes pulser {
  50% { opacity: 0.35; }
}

.boutons {
  display: flex;
  gap: 16px;
  justify-content: center;
  flex-wrap: wrap;
}

/* le reste de l'accueil apparaît après que mon nom a été tapé */
.apres {
  animation: apparaitre 0.8s ease backwards;
  animation-delay: 2.4s;
}

.apres-2 {
  animation-delay: 2.7s;
}

.apres-3 {
  animation-delay: 3s;
}

@keyframes apparaitre {
  from {
    opacity: 0;
    transform: translateY(12px);
  }
}

/* ----- mes sections ----- */
.bloc {
  padding-top: 72px;
  padding-bottom: 72px;
}

h2 {
  margin: 0 0 16px;
  font-size: 2rem;
}

h3 {
  margin: 0 0 6px;
  font-size: 1.1rem;
}

.texte {
  max-width: 65ch;
  margin: 0 0 12px;
  color: var(--couleur-texte-doux);
}

/* une section "revele" est cachée, puis elle monte doucement quand on arrive dessus */
.revele {
  opacity: 0;
  transform: translateY(24px);
}

.revele.visible {
  opacity: 1;
  transform: none;
  transition: opacity 0.6s ease, transform 0.6s ease;
}

/* mon animation d'entrée, partagée par les pastilles et les fenêtres */
@keyframes entrer {
  from {
    opacity: 0;
    transform: translateY(16px);
  }
}

/* ----- à propos : je présente mes faits comme des clés et des valeurs ----- */
.faits {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(210px, 1fr));
  gap: 24px;
  margin-top: 40px;
}

.fait {
  padding-top: 16px;
  border-top: 1px solid var(--couleur-bordure);
}

.fait h3 {
  color: var(--code-bleu);
  font-family: var(--police-code);
  font-size: 0.95rem;
  font-weight: 600;
}

.fait h3::after {
  content: ':';
  color: var(--code-gris);
}

.fait p {
  margin: 0;
  color: var(--couleur-texte-doux);
}

/* ----- compétences ----- */
.groupe {
  margin-top: 28px;
}

.groupe h3 {
  margin-bottom: 12px;
  color: var(--couleur-texte-doux);
  font-family: var(--police-code);
  font-size: 0.9rem;
  font-weight: 600;
}

.chips {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}

/* une pastille cachée, avant que la section soit visible */
.chip {
  padding: 5px 12px;
  border: 1px solid var(--couleur-bordure);
  border-radius: 6px;
  background-color: var(--couleur-surface);
  color: var(--couleur-texte);
  font-family: var(--police-code);
  font-size: 0.85rem;
  opacity: 0;
  transition: border-color 0.2s, color 0.2s;
}

/* quand la section est visible, chaque pastille apparaît l'une après l'autre */
.visible .chip {
  opacity: 1;
  animation: entrer 0.4s ease backwards;
  animation-delay: calc(var(--i) * 0.06s);
}

.chip:hover {
  border-color: var(--code-bleu);
  color: var(--code-bleu);
}

/* ----- projets ----- */
.projets {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 20px;
  margin-top: 32px;
}

/* une fenêtre cachée, avant que la section soit visible */
.carte-projet {
  opacity: 0;
}

/* quand la section est visible, chaque fenêtre se pose l'une après l'autre */
.visible .carte-projet {
  opacity: 1;
  animation: entrer 0.6s ease backwards;
  animation-delay: calc(var(--i) * 0.12s);
}

.carte-projet:hover {
  border-color: var(--couleur-texte-doux);
}

.ecole {
  margin: 0 0 6px;
  color: var(--code-gris);
  font-family: var(--police-code);
  font-size: 0.8rem;
}

.ecole::before {
  content: '// ';
}

.carte-projet h3 {
  font-size: 1.25rem;
}

.resume {
  margin: 8px 0 0;
  color: var(--couleur-texte-doux);
}

.tags {
  display: flex;
  flex-wrap: wrap;
  gap: 8px 16px;
  margin-top: 16px;
}

.tag {
  color: var(--code-orange);
  font-family: var(--police-code);
  font-size: 0.8rem;
}

/* ----- expérience ----- */
.carte-experience {
  max-width: 720px;
  margin-top: 32px;
}

.badge {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  margin: 0 0 12px;
  color: var(--code-vert);
  font-family: var(--police-code);
  font-size: 0.8rem;
}

.carte-experience h3 {
  font-size: 1.25rem;
}

.entreprise {
  margin: 0 0 16px;
  color: var(--couleur-texte-doux);
}

.carte-experience ul {
  margin: 0;
  padding-left: 20px;
  color: var(--couleur-texte-doux);
}

.carte-experience li {
  margin-bottom: 6px;
}

/* ----- contact ----- */
.contact {
  max-width: 720px;
  text-align: center;
}

.contact .texte {
  margin-left: auto;
  margin-right: auto;
}

.contact .boutons {
  margin-top: 24px;
}

.lieu {
  margin: 24px 0 0;
  color: var(--couleur-texte-doux);
  font-family: var(--police-code);
  font-size: 0.85rem;
}

/* si la personne a demandé moins d'animations, je coupe tout */
@media (prefers-reduced-motion: reduce) {
  .point,
  .apres,
  .visible .chip,
  .visible .carte-projet {
    animation: none;
  }

  .revele.visible {
    transition: none;
  }
}
</style>