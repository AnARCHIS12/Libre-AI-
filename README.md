<p align="center">
  <img src="https://img.shields.io/badge/Libre%20AI-Personal%20Mistral%20Chatbot-ff1744?style=for-the-badge&labelColor=050101" alt="Libre AI">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/HTML5-single%20file-ff3b30?style=flat-square&labelColor=111111" alt="HTML5 single file">
  <img src="https://img.shields.io/badge/JavaScript-vanilla-ff8a3d?style=flat-square&labelColor=111111" alt="Vanilla JavaScript">
  <img src="https://img.shields.io/badge/Mistral%20AI-API-ff1744?style=flat-square&labelColor=111111" alt="Mistral AI API">
  <img src="https://img.shields.io/badge/IndexedDB-local%20storage-b00020?style=flat-square&labelColor=111111" alt="IndexedDB local storage">
  <img src="https://img.shields.io/badge/backend-none-202020?style=flat-square&labelColor=111111" alt="No backend">
  <img src="https://img.shields.io/badge/theme-red%20black-ff1744?style=flat-square&labelColor=050101" alt="Red black theme">
</p>

# Libre AI

Libre AI est une application web locale pour discuter avec les modèles Mistral AI. Elle tient dans un seul fichier `index.html`, sans backend, sans installation npm, et stocke vos conversations, agents, paramètres et mémoires dans le navigateur.

## Fonctionnalités

- Application autonome en HTML, CSS et JavaScript vanilla.
- Appels directs à l'API `https://api.mistral.ai/v1/chat/completions`.
- Support de plusieurs modèles Mistral, dont modèles texte, code, vision et audio selon disponibilité API.
- Mémoire globale persistante avec IndexedDB.
- Agents spécialisés créés manuellement ou générés automatiquement avec Mistral.
- Import/export complet des données en JSON.
- Interface rouge/noir par défaut, avec thème personnalisable pendant la configuration initiale.
- Icônes Font Awesome, polices Fontsource et Bootstrap servis via jsDelivr.

## Installation

### Usage local

1. Ouvrez `index.html` dans Chrome, Firefox, Edge ou Safari.
2. Entrez votre clé API Mistral au premier lancement.
3. Configurez le nom, l'objectif et les couleurs de votre assistant.

### Hébergement statique

Vous pouvez aussi héberger `index.html` sur GitHub Pages, Netlify, Vercel ou n'importe quel serveur statique.

## Clé API Mistral

1. Allez sur `https://console.mistral.ai`.
2. Créez un compte ou connectez-vous.
3. Ouvrez la section `API Keys`.
4. Créez une nouvelle clé, par exemple `Libre-AI-Personal`.
5. Copiez la clé et collez-la dans Libre AI.

La clé est stockée localement dans un cookie et dans `localStorage` en fallback. Elle est uniquement utilisée pour appeler l'API Mistral.

## Configuration initiale

Le wizard intégré comporte trois étapes :

1. Saisie et validation de la clé API.
2. Personnalisation de l'assistant : nom, objectif, couleurs primaire/secondaire/accent.
3. Génération automatique de 20 agents spécialisés avec Mistral Large.

La génération d'agents peut être ignorée si vous préférez créer vos agents manuellement.

## Données locales

Libre AI utilise IndexedDB avec quatre stores :

```javascript
const DB_NAME = "VOANH_AI_DB"; // nom historique conservé pour ne pas perdre les données locales existantes
const DB_VERSION = 3;

// chats: conversations et messages
// agents: agents personnalisés
// global_memory: mémoire globale
// settings: thème, modèle, configuration IA, chat courant
```

Le nom `VOANH_AI_DB` est volontairement conservé pour assurer la compatibilité avec les anciennes données locales.

## Mémoire globale

La mémoire globale permet de conserver des informations importantes entre les conversations.

Elle sert à :

- stocker des faits utiles ;
- enrichir les futures réponses avec du contexte ;
- partager une mémoire entre tous les chats ;
- supprimer les entrées obsolètes depuis le panneau Mémoire.

Les mémoires restent dans IndexedDB et ne quittent le navigateur que si elles sont incluses dans une requête envoyée à Mistral pour contextualiser une réponse.

## Agents

Un agent est un profil spécialisé qui modifie le prompt système.

Un agent peut contenir :

- nom et description ;
- instructions détaillées ;
- tags ;
- style de réponse ;
- température ;
- modèle préféré ;
- règles ou interdictions ;
- primer personnel.

Vous pouvez créer, modifier, dupliquer, supprimer, importer ou exporter des agents.

## Import et export

L'export complet crée un fichier :

```text
libre-ai-backup-YYYY-MM-DD.libre-ai.json
```

Ce fichier peut contenir :

- conversations ;
- agents ;
- mémoire globale ;
- paramètres ;
- thème personnalisé.

L'import accepte les fichiers `.libre-ai.json`, `.voanh.json` et `.json` pour garder la compatibilité avec les anciennes sauvegardes.

Les agents individuels peuvent aussi être exportés au format :

```text
agent-NomDeLAgent.json
```

## Confidentialité

- Aucun serveur backend n'est utilisé.
- Les conversations, agents, mémoires et paramètres restent dans le navigateur.
- Les requêtes IA sont envoyées directement à `api.mistral.ai`.
- Les CDN utilisés servent uniquement les assets frontend : Bootstrap, Font Awesome et Fontsource via jsDelivr.
- Aucune collecte analytics n'est incluse dans le code.

## Personnalisation

Vous pouvez personnaliser :

- les couleurs dans le wizard initial ou via le thème `CUSTOM` ;
- les modèles dans le tableau `MODELS` ;
- les prompts dans `buildSystemPrompt()` ;
- l'apparence via les variables CSS dans `:root`.

Couleurs par défaut :

```css
:root {
  --cyan: #ff1744;
  --neon: #ff3b30;
  --plasma: #ff8a3d;
}
```

## Structure technique

- `index.html` : application complète.
- `README.md` : documentation courte.
- `.gitignore` : exclusions Git.

Il n'y a pas de build, pas de serveur Node, pas de dépendances locales à installer.

## Crédits

- Moteur IA : Mistral AI
- UI : Bootstrap 5.3
- Icônes : Font Awesome via jsDelivr
- Polices : Fontsource via jsDelivr
- Licence : MIT, voir `LICENSE`
