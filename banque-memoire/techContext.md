# Contexte Technique

## Stack Technologique

### HTML
- HTML5 sémantique
- Meta tags pour SEO et viewport
- Structure monopage (single-file)

### CSS
- **CSS pur** (pas de frameworks comme Bootstrap, Tailwind)
- Variables CSS (:root) pour la cohérence des couleurs
- Media queries pour responsive design
- Animations CSS (keyframes) pour transitions
- Flexbox pour layouts

### JavaScript
- **Vanilla JS** (pas de jQuery, React, etc.)
- ES6+ (const, let, arrow functions, template literals)
- localStorage pour persistance du compteur
- requestAnimationFrame pour animations fluides
- Event delegation et listeners optimisés

## Dépendances Externes

### Fonts Google
- **Amiri** (400, 700) - Pour le texte arabe
- **Lato** (400, 700) - Pour le texte latin
- **Scheherazade New** (400, 700) - Alternative pour l'arabe

**Chargement optimisé** :
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=..." rel="stylesheet">
```

## Configuration de Développement

### Contraintes GitHub Pages
- Hébergement statique
- Pas de backend
- Pas de PHP, Node.js, etc.
- Fichier unique index.html
- Images locales (profil.jpg)

### Responsive Breakpoints
- **Mobile** : max-width: 600px
- **Tablet** : 601px - 900px
- **Desktop** : min-width: 901px

## Préférences de Codage

### Conventions CSS
- Variables CSS pour les couleurs (préfixe --)
- Nommage en kebab-case (class="tab-btn")
- Groupement logique avec commentaires
- Mobile-first approach

### Conventions JavaScript
- Fonctions nommées (pas de fonctions anonymes sauf callback)
- camelCase pour les variables et fonctions
- Commentaires pour sections complexes
- Gestion d'erreurs avec try/catch où approprié

### Accessibilité
- Contrast ratio minimum 4.5:1 pour le texte
- Focus states visibles
- Labels pour les inputs
- Aria labels si nécessaire
- Semantic HTML (header, nav, main, section, footer)

## Modèles d'Utilisation

### Gestion des Onglets
```javascript
function openTab(evt, tabName) {
  // Cacher tous les contenus
  // Désactiver tous les boutons
  // Activer l'onglet choisi
  // Activer le bouton correspondant
}
```

### Filtrage des Cartes
```javascript
function filterCards() {
  // Récupérer la valeur de recherche
  // Parcourir toutes les cartes
  // Comparer avec keywords et textContent
  // Ajouter/retirer classe .hidden
}
```

### Compteur de Dhikr (v2 - Bouton Reset + Modale Custom)
```javascript
// Pattern anti-double-compte sur mobile
let touchFired = false;

// Touch events (mobile) - prioritaires
counter.addEventListener('touchend', (e) => {
    if (e.target === resetBtn || e.target.closest('.reset-modal')) return;
    e.preventDefault();
    touchFired = true;
    incrementCounter();
});

// Mouse events (desktop) - ignorés si touch déjà traité
counter.addEventListener('click', (e) => {
    if (e.target === resetBtn || e.target.closest('.reset-modal')) return;
    if (touchFired) {
        touchFired = false;  // Reset du flag
        return;              // Ignorer le clic
    }
    incrementCounter();
});

// Modale custom (remplace confirm())
function showResetModal() {
    resetModal.classList.add('active');
    resetOverlay.classList.add('active');
}

function hideResetModal() {
    resetModal.classList.remove('active');
    resetOverlay.classList.remove('active');
}

function doReset() {
    document.getElementById('global-count').textContent = '0';
    localStorage.setItem('global_counter', 0);
    hideResetModal();
}
```

**Structure HTML du compteur** :
```html
<div class="reset-overlay" id="resetOverlay"></div>
<div id="global-counter">
    <button class="reset-btn" id="resetBtn">R</button>
    <div class="reset-modal" id="resetModal">
        <p>Réinitialiser le compteur ?</p>
        <div class="reset-modal-btns">
            <button class="btn-cancel" id="cancelReset">Annuler</button>
            <button class="btn-confirm" id="confirmReset">Effacer</button>
        </div>
    </div>
    <span class="count" id="global-count">0</span>
    <span class="label">dhikr</span>
</div>
```

## Performances

### Optimisations
- CSS critique inline (pour le fold)
- Lazy loading des images (si applicable)
- Minification en production (optionnel)
- Compression gzip activée sur GitHub Pages

### Budget de Performance
- Temps de chargement initial < 2 secondes
- Taille fichier < 100KB (sans images)
- FPS animation > 60fps
