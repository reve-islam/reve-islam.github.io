# Patterns Système

## Architecture du Site

### Structure Principale
- **Page monopage** (Single Page Application-like)
- Système d'onglets pour organiser les 3 sections : Rêves, Diagnostic, Invocations
- Navigation sticky pour rester accessible pendant le scroll

### Composants Clés

#### 1. Système d'Onglets
- 3 onglets : Rêves (bleu), Diagnostic (violet), Invocations (vert)
- Activation par click avec animation fade-in
- Code couleur distinctif pour chaque section
- Navigation sticky (z-index: 100)

#### 2. Contrôles de Recherche (Onglet Invocations)
- Menu déroulant d'accès rapide (scroll vers la carte)
- Champ de recherche textuel (filtrage en temps réel)
- Position sticky sous les onglets (z-index: 90)
- Compatible mobile et desktop

#### 3. Cartes d'Invocations
- Structure individuelle (une invocation par carte)
- Composants par carte :
  - Titre + tag catégorie
  - Texte arabe (font Amiri/Scheherazade)
  - Translittération (italique)
  - Traduction française
  - Instructions de récitation (nombre de fois, modalité)
- Scroll margin-top pour éviter le masquage par le header sticky

#### 4. Compteur de Dhikr Global
- Bouton circulaire fixe en bas à droite (65px)
- Incrément par clic court
- Reset par appui long (2 secondes) avec indicateur visuel de progression
- Persistance via localStorage
- Animation feedback sur clic (scale)

#### 5. Section de Paiement
- 3 méthodes : Western Union, Remitly, Taptap Send
- Bouton WhatsApp pour envoyer la preuve
- Grid layout pour les cartes de paiement
- Liens directs vers les sites de transfert

## Modèles de Données

### Structure d'une Invocation (Card)
```html
<div class="card" id="card-id" data-title="Titre" data-keywords="mots-clés">
  <h3>Titre <span class="category-tag">Catégorie</span></h3>
  <div class="arabic-text">Texte arabe complet</div>
  <div class="transliteration">Translittération</div>
  <div class="translation">Traduction</div>
  <div class="instruction">Instructions (répétitions)</div>
</div>
```

### Données de Paiement
- Western Union : Nom + Ville + MTCN
- Remitly : Nom + Numéro (Mvola) + Opérateur
- Taptap Send : Nom + Service recommandé

## Flux Utilisateur Typique

1. **Utilisateur arrive** sur la page → Voir le profil et les 3 onglets
2. **Navigate vers l'onglet souhaité** → Onglet s'active avec animation
3. **Si Invocations** → Utilise le menu ou la recherche
4. **Lit l'invocation** → Peut utiliser le compteur de dhikr global
5. **Si service payant** → Scrolle vers le bas → Choisit méthode de paiement → Envoie preuve sur WhatsApp

## Optimisations de Performance
- CSS pur (pas de frameworks)
- Fonts Google avec preconnect
- Animations légères (transform, opacity)
- JavaScript minimal et optimisé
- Aucune dépendance externe lourde
