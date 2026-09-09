# Design System — D&D Wireframes

## Charte Graphique

### Dark Mode Natif
Unique mode (pas de light mode option).

### Palette
Voir `colors.json`

### Typographies
- Font: Inter (Variable, Regular à SemiBold)
- Min 16px pour texte interactif (mobile)
- Valeurs chiffrées: tabulaires, chasse resserrée

### Iconographie
Lucide Icons — voir `icons-lucide.txt`

## Layout

### Breakpoints
- Mobile: 375px (Dashboard Joueur ref)
- Tablet: 1024px (Dashboard MJ responsive)
- Desktop: 1440px (Dashboard MJ ref)

### Grille MJ
```css
grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4
```

### Responsivité
Aucune navigation persistante.
Règle des 10 secondes (info vitale en < 1 tap).

## Tokens Tailwind
Voir `tokens-tailwind.json`

Usage:
```jsx
<div className="bg-bg-primary text-text-primary">
  <div className="border border-border-subtle rounded">
    <span className="text-state-healthy">Saine</span>
  </div>
</div>
```

## Écrans (Phase 3.1 — Basse Fidélité)

1. Dashboard Joueur (mobile 375px)
2. Dashboard MJ (desktop 1440px / tablet 1024px)
3. Modale Vue Détaillée (overlay)
4. Formulaire Création Personnage (mobile 375px)
5. Écrans d'Entrée (Accueil/Connexion)

Wireframes = noir & blanc strict (couleur appliquée en Phase 3.2).
