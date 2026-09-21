# Design System — D&D Ops

## 1. Charte Graphique

### Dark Mode natif
Non optionnel. Pensé pour un usage en conditions de faible luminosité 
(sessions de jeu en soirée).

### Palette
Voir `colors.json` pour le détail complet (hex + usage + règles de non-collision).

### Typographies
- Police unique : **Inter** (variable, Regular à SemiBold) — limite le poids 
  de chargement et la complexité d'intégration
- Valeurs chiffrées dynamiques (PV, CA, bonus d'attaque, BBA) : variante à 
  chasse resserrée, chiffres tabulaires — affichage stable lors des mises 
  à jour temps réel
- Taille minimale : **16px** pour tout élément de texte interactif sur mobile

### Iconographie
- Bibliothèque : **Lucide Icons** (pack libre et statique, conforme à la 
  contrainte d'absence d'API tierce payante ou d'IA en V1)
- Usage strictement fonctionnel : un pictogramme = une seule notion dans 
  toute l'application
- Aucune icône décorative (préserve la lisibilité de la Grid MJ en 
  configuration dense — US-07 CA-03)

**Mapping conceptuel (noms d'icônes Lucide à préciser à l'usage) :**
| Notion | Concept |
|---|---|
| Classe d'Armure (CA) | bouclier |
| Jet de dé / initiative | dé |
| Arme | épée |
| Compétence passive | œil |
| Statut préjudiciable | éclair |

## 2. Design System Tokens (Tailwind CSS)

Voir `tokens-tailwind.json` pour la structure complète.

**Principe directeur :** aucune couleur n'est utilisée "en dur" dans les 
composants ; toute référence passe par un token nommé (ex. `bg-state-critical`, 
`text-accent-turn`), garantissant un point de vérité unique pour toute 
évolution future de la charte.

Groupes de tokens :
- `colors.bg` : primary, surface, surface-raised
- `colors.border` : subtle
- `colors.text` : primary, muted
- `colors.state` : healthy, wounded, critical, dying, buff, debuff
- `colors.accent` : turn
- `fontFamily.sans` : Inter
- `fontSize` : stat-lg, stat-md (tailles dédiées aux valeurs chiffrées clés)

## 3. Écrans & Structure (Wireframes — Phase 3.1)

### Cadrage général
Processus en 3 phases : Zoning → Wireframe (basse fidélité) → Design Final 
(haute fidélité), appliqué dans le même ordre d'écrans à chaque phase.

**Contraintes transversales :**
- Dashboard Joueur : mobile-first strict (référence 375px), pas de variante desktop
- Dashboard MJ : desktop/tablette en priorité, repli mobile natif via grille Tailwind
- Dark Mode natif : pas de variante "mode clair"
- Aucune navigation persistante ni menu — **4 écrans réels + 1 état modal**

**Ordre de traitement :**
1. Dashboard Joueur
2. Dashboard MJ
3. Modale Vue Détaillée
4. Formulaire de création de personnage
5. Écran d'entrée (unique, avec sélecteur de rôle Joueur/MJ)

---

### Dashboard Joueur ("Télécommande") — mobile 375px

**Zoning :**
Header/Changement Campagne → Bannière initiative (conditionnelle) → 
Identité (Nom/Classe/Niveau + statuts) → Armes → Ressources → 
Caractéristiques → Défense (CA/JdS) → Zone vitale (PV + Modificateur 
Temporaire Global), **fixe en bas d'écran**

**Contenu hiérarchisé (scroll unique strict) :**
1. Bannière d'initiative (si combat)
2. Identité + badges de statuts
3. Cartes d'armes (BBA + séquence itérative)
4. Ressources/capacités
5. Caractéristiques
6. Classe d'Armure (CA) et Jets de Sauvegarde (JdS)
7. Bonus d'initiative (brut)

**Zone vitale — architecture fixe :**
La zone vitale (jauge de PV actuels/max/temporaires, boutons Dégâts/Soins, 
et Modificateur Temporaire Global) constitue un **pied de page fixe**, 
ancré en bas de l'écran en permanence, indépendant du scroll du contenu 
au-dessus. Le Modificateur Temporaire Global est intégré à cette zone 
fixe (US-01, US-03).

---

### Dashboard MJ — desktop 1440 / tablette 1024

**Zoning :**
Header/Changement Campagne → Bascule Exploration/Combat → 
Barre d'Initiative (si combat actif) → Grid des PlayerCards

**Contenu hiérarchisé :**
1. Bascule Exploration/Combat
2. Barre d'Initiative (si combat)
3. Grid des PlayerCards (identité, PV condensé, statuts, CA/JdS modifiés, DET/FOU/PSY)

Grille responsive : `grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4`

---

### Modale Vue Détaillée (MJ)

**Zoning :**
En-tête (identité + PV + statuts) → Défense → Compétences passives → 
Caractéristiques → Armes → Ressources

**Contenu hiérarchisé :**
1. En-tête (identité, PV, statuts)
2. Défense (CA/JdS + Modificateur — **seul champ éditable de la modale**)
3. Compétences passives
4. Caractéristiques
5. BBA/Armes
6. Ressources
7. Fermeture

---

### Formulaire de création de personnage — mobile 375px

**Zoning :**
Identité → Points de vie → Caractéristiques/CA/JdS → BBA/Armes → 
Ressources → Compétences passives → Validation

**Contenu hiérarchisé — 7 zones :**
1. Identité (Nom/Classe/Niveau)
2. Points de vie (PV max/actuels/temporaires)
3. Caractéristiques/CA/JdS
4. BBA/Armes
5. Ressources
6. Compétences passives
7. Validation unique (bouton unique en bas de page)

One-page, sans wizard. Traversé une seule fois par joueur et par campagne.

---

### Écran d'entrée (unique)

Fusion de l'ancien parcours en 3 écrans (Accueil / Connexion MJ / 
Identification Joueur) en **un seul écran combiné** :

- Nom de l'application + panneau "À quoi ça sert ?" escamotable
- Sélecteur segmenté de rôle : [Joueur] / [MJ]
- Champ Code de campagne
- Champ Pseudo (affiché uniquement si rôle = Joueur)
- Bouton d'action unique

**2 états :**
- **Nouveau visiteur** : panneau déplié, champs vides, bouton [Entrer]
- **Appareil connu** : panneau replié, champs pré-remplis (localStorage), 
  bouton [Reprendre la partie], lien [Changer de campagne]

---

## 4. Principes transversaux

- Dark Mode natif (obligatoire)
- Mobile-first pour Dashboard Joueur (375px référence)
- Desktop-first pour Dashboard MJ (1440px référence)
- Aucune navigation persistante
- Règle des 10 secondes (accès rapide aux infos vitales)
- Responsive via grille Tailwind (pas de variante desktop séparée)
- Badges textuels obligatoires pour statuts critiques (jamais couleur seule)
- Wireframe = noir et blanc strict (charte graphique appliquée en Phase 3.2)
