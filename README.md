# 🌐 Portfolio — Isaac Damas GAHOU

> Portfolio professionnel en ligne d'Isaac Damas GAHOU, Ingénieur Énergéticien & Procédés, spécialisé en systèmes solaires PV hors réseau. Accessible à l'adresse : **[isaac-gahou.vercel.app](https://isaac-gahou.vercel.app)**

---

## 📋 Description du projet

Site web portfolio **single-page** (une seule page HTML) avec panneau d'administration intégré, connecté à une base de données **Supabase** et hébergé sur **Vercel**. Le contenu est entièrement dynamique et modifiable sans toucher au code, via un espace admin sécurisé par mot de passe.

Le site a été conçu pour deux objectifs principaux :
- **Trouver des opportunités freelance** (clients européens, ONG, bureaux d'études)
- **Attirer des recruteurs** pour des bourses internationales et postes d'ingénieur senior

---

## 🗂️ Structure du projet

```
portfolio-gahou/
│
├── index.html          # Site complet (HTML + CSS + JS en un seul fichier)
└── README.md           # Ce fichier
```

### Pourquoi un seul fichier HTML ?

Le choix d'un fichier HTML unique (sans framework, sans build system) est délibéré :
- **Zéro dépendance** — aucun `npm install`, aucun framework à maintenir
- **Déploiement instantané** — Vercel sert le fichier statique directement
- **Modifiable partout** — n'importe quel éditeur texte suffit
- **Performances** — chargement ultra-rapide, pas de bundle JS lourd

---

## 🛠️ Stack technique

| Composant | Technologie | Rôle |
|---|---|---|
| Frontend | HTML5 + CSS3 + JavaScript Vanilla | Interface utilisateur |
| Base de données | Supabase (PostgreSQL) | Stockage du contenu dynamique |
| Hébergement | Vercel | Déploiement et CDN mondial |
| Versioning | GitHub (`DamasBuffy99/portfolio-gahou`) | Source de vérité + CI/CD |
| Fonts | Google Fonts (Space Mono + Inter) | Typographie |
| Markdown | marked.js (CDN) | Rendu des articles de blog |

---

## 🗄️ Base de données Supabase

**Projet ID** : `yqvwmiidmxjiupigaujy`
**Région** : `eu-west-1` (Europe Ouest)
**URL** : `https://yqvwmiidmxjiupigaujy.supabase.co`

### Tables

#### `profile`
Informations personnelles affichées sur le site (hero, contact, stats).

| Colonne | Type | Description |
|---|---|---|
| `id` | uuid | Clé primaire |
| `name` | text | Nom complet |
| `title` | text | Titre professionnel |
| `bio` | text | Présentation |
| `location` | text | Localisation |
| `email` | text | Email de contact |
| `phone` | text | Téléphone |
| `linkedin_url` | text | URL profil LinkedIn |
| `stat_years` | text | Stat "Années d'expérience" |
| `stat_kwc` | text | Stat "kWc installés" |
| `stat_sites` | text | Stat "Sites réalisés" |
| `updated_at` | timestamptz | Dernière mise à jour |

#### `blog_posts`
Articles du blog, avec support Markdown complet.

| Colonne | Type | Description |
|---|---|---|
| `id` | uuid | Clé primaire |
| `title` | text | Titre de l'article |
| `slug` | text | URL friendly unique |
| `excerpt` | text | Résumé court affiché sur la card |
| `content` | text | Contenu complet en Markdown |
| `tag` | text | Catégorie (ex: SYSTÈMES PV, ONDULEURS) |
| `read_time` | text | Temps de lecture estimé |
| `published` | boolean | true = public, false = brouillon |
| `created_at` | timestamptz | Date de création |
| `updated_at` | timestamptz | Dernière modification |

#### `projects`
Réalisations terrain affichées dans la section Projets.

| Colonne | Type | Description |
|---|---|---|
| `id` | uuid | Clé primaire |
| `title` | text | Nom du projet |
| `description` | text | Description courte |
| `kwc` | text | Puissance ou référence (ex: 30 kWc ×2) |
| `type_label` | text | Badge type (ex: OFF-GRID, URGENCE) |
| `meta` | text | Contexte (ex: AdMec CTIB · 2024) |
| `badges` | text[] | Tags techniques |
| `display_order` | int | Ordre d'affichage |
| `active` | boolean | Visible ou masqué |

#### `certifications`
Diplômes et certifications.

| Colonne | Type | Description |
|---|---|---|
| `id` | uuid | Clé primaire |
| `title` | text | Intitulé de la certification |
| `issuer` | text | Organisme émetteur |
| `date_label` | text | Date lisible (ex: MARS 2026) |
| `icon` | text | Emoji représentatif |
| `display_order` | int | Ordre d'affichage |

### Row Level Security (RLS)

Toutes les tables ont le RLS activé :
- **Lecture publique** : tout le monde peut lire les données publiées
- **Écriture** : ouverte via la clé anon, sécurisée côté app par le mot de passe admin

---

## 🔐 Panneau d'administration

Le site intègre un **panneau admin complet** sans page externe.

### Accès
- Ouvrir la console du navigateur (F12)
- Taper : `openAdmin()`
- Mot de passe : `gahou2026!`

Le bouton Admin a été volontairement retiré de la navbar pour ne pas être visible des visiteurs.

### Fonctionnalités admin

| Onglet | Actions disponibles |
|---|---|
| 👤 Profil | Modifier nom, titre, bio, email, téléphone, LinkedIn, stats hero |
| ✍ Blog | Créer / modifier / supprimer des articles, gérer brouillons |
| 🔧 Projets | Créer / modifier / supprimer des projets |
| 🎓 Certifications | Créer / modifier / supprimer des certifications |

### Éditeur de blog
L'éditeur accepte du **Markdown complet** : titres, tableaux, listes, gras, italique, code inline.

---

## 🚀 Déploiement

### Workflow CI/CD automatique

```
Modification du code
        ↓
Push sur GitHub (branche main)
        ↓
Vercel détecte le push automatiquement
        ↓
Rebuild et redéploiement (~30 secondes)
        ↓
Site mis à jour sur isaac-gahou.vercel.app
```

### Faire une mise à jour frontend

```bash
git add index.html
git commit -m "Description de la modification"
git push origin main
```

Vercel redéploie automatiquement après chaque push.

### Variables d'environnement

Aucune variable d'environnement requise. La clé Supabase `anon` (publique par nature) est directement dans le code HTML — comportement standard pour les clés Supabase côté client.

---

## 🎨 Design

### Palette de couleurs

| Variable CSS | Valeur | Usage |
|---|---|---|
| `--teal` | `#0a9396` | Couleur principale, accents |
| `--teal-light` | `#94d2bd` | Textes secondaires colorés |
| `--teal-dark` | `#005f61` | Hover, éléments discrets |
| `--amber` | `#e9d8a6` | Accents chauds, entreprises, dates |
| `--bg` | `#001219` | Fond principal (très sombre) |
| `--bg2` | `#012a32` | Fond sections alternées |
| `--bg3` | `#0d3b44` | Cards, blocs imbriqués |
| `--text` | `#e0f0f1` | Texte principal |
| `--muted` | `#7aadae` | Texte secondaire |

### Typographie

- **Space Mono** — titres, labels, éléments techniques (identité ingénieur)
- **Inter** — corps de texte, descriptions

### Sections du site

1. **Hero** — Terminal animé typewriter + nom + stats clés
2. **À propos** — Bio + blocs de specs techniques
3. **Compétences** — 4 cards avec barres de progression
4. **Expérience** — Timeline verticale avec badges
5. **Projets** — Grille dynamique (Supabase)
6. **Certifications** — Grille dynamique (Supabase)
7. **CV** — Bouton téléchargement PDF
8. **Blog** — Articles dynamiques avec lecteur Markdown (Supabase)
9. **Contact** — Email, LinkedIn, CV

---

## 📝 Contenu blog

| Titre | Tag | Statut |
|---|---|---|
| Guide complet des onduleurs solaires | SYSTÈMES PV | ✅ Publié |
| Dimensionner une minicentrale off-grid pour site télécom | SYSTÈMES PV | 📝 Brouillon |
| Deye Master/Slave : configuration et monitoring | ONDULEURS | 📝 Brouillon |
| Devenir ingénieur solaire en Afrique de l'Ouest | CARRIÈRE | 📝 Brouillon |

---

## 🔧 Évolutions prévues

- [ ] Formulaire de contact fonctionnel (Resend ou Supabase Edge Functions)
- [ ] Domaine personnalisé (isaacgahou.com ou similaire)
- [ ] Authentification Supabase Auth pour sécuriser l'admin
- [ ] Version anglaise du site
- [ ] Section "Services freelance" avec tarifs
- [ ] Page de détail article avec URL propre (/blog/slug)

---

## 👤 Auteur

**Isaac Damas GAHOU**
Ingénieur Énergéticien & Procédés — AdMec CTIB, Cotonou, Bénin
📧 igahou22@gmail.com
🔗 [isaac-gahou.vercel.app](https://isaac-gahou.vercel.app)
💼 [LinkedIn](https://www.linkedin.com/in/isaac-gahou)
🐙 [GitHub](https://github.com/DamasBuffy99)
