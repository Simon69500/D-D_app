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
