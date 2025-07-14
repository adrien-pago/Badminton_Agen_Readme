# Badminton Agen - Site Web

Site web moderne pour le club de badminton d'Agen, développé avec Symfony 6.4 et Webpack Encore.

## 🚀 Technologies Utilisées

- **Symfony 6.4** (LTS) - Framework PHP
- **Twig** - Moteur de templates
- **Webpack Encore** - Gestion des assets
- **SCSS** - Préprocesseur CSS
- **JavaScript ES6+** - Interactivité côté client
- **FontAwesome** - Icônes modernes

## 📁 Structure du Projet

```
Badminton_Agen/
├── assets/
│   ├── styles/
│   │   ├── base/           # Variables, reset, styles de base
│   │   ├── components/     # Composants réutilisables
│   │   ├── layout/         # Layouts et structure
│   │   ├── pages/          # Styles spécifiques aux pages
│   │   └── app.scss        # Fichier principal SCSS
│   └── app.js              # JavaScript principal
├── src/
│   └── Controller/         # Contrôleurs modulaires
│       ├── Club/
│       ├── Equipe/
│       ├── Tournoi/
│       ├── Bureau/
│       ├── Actualite/
│       ├── Evenement/
│       ├── Contact/
│       ├── Gymnase/
│       ├── Licence/
│       ├── Reseaux/
│       ├── Entrainement/
│       └── Gallery/
├── templates/              # Templates Twig
│   ├── base.html.twig     # Template de base
│   ├── home/              # Page d'accueil
│   └── [modules]/         # Templates par module
└── public/                # Assets compilés
```

## 🛠️ Installation

### Prérequis

- PHP 8.1+
- Composer
- Node.js 16+
- npm ou yarn

### Étapes d'installation

1. **Cloner le projet**
   ```bash
   git clone [URL_DU_REPO]
   cd Badminton_Agen
   ```

2. **Installer les dépendances PHP**
   ```bash
   composer install
   ```

3. **Installer les dépendances Node.js**
   ```bash
   npm install
   ```

4. **Configurer l'environnement**
   ```bash
   cp .env .env.local
   # Éditer .env.local avec vos paramètres
   ```

5. **Créer la base de données (optionnel)**
   ```bash
   php bin/console doctrine:database:create
   php bin/console doctrine:migrations:migrate
   ```

## 🚀 Commandes de Base

### Développement

```bash
# Démarrer le serveur de développement Symfony
symfony server:start

# Compiler les assets en mode développement
npm run dev

# Compiler les assets en mode production
npm run build

# Surveiller les changements d'assets
npm run watch
```

### Production

```bash
# Compiler les assets pour la production
npm run build

# Optimiser les assets
npm run build -- --optimize
```

### Maintenance

```bash
# Vider le cache
php bin/console cache:clear

# Vider le cache en production
php bin/console cache:clear --env=prod

# Mettre à jour les dépendances
composer update
npm update
```

## 📱 Fonctionnalités

### Navigation Moderne
- **Sidebar latérale responsive** (mobile ET desktop)
- **Menu burger agrandi** toujours visible en haut à gauche
- **Overlay sombre** quand la sidebar est ouverte
- **Fermeture multiple** : croix, overlay, touche Echap, clic lien
- **Icônes FontAwesome** pour tous les menus
- **Expérience identique** sur mobile et desktop

### Page d'Accueil
- **Titre moderne** avec soulignement animé et espacement optimisé
- **Section réseaux sociaux** sous le titre avec logos cliquables
- **9 cartes cliquables** : Présentation, Équipes, Tournois, Bureau, Actualités, Événements, Contact, Gymnase, Licence
- **Design mobile-first** avec animations fluides
- **Aucun scroll horizontal** - layout parfaitement responsive

### Modules Disponibles
- **Club** : Présentation du club, histoire, valeurs
- **Équipes** : Toutes les équipes et leurs performances
- **Tournois** : Calendrier et résultats des compétitions
- **Bureau** : Membres du bureau et organisation
- **Actualités** : Dernières nouvelles du club
- **Événements** : Manifestations et activités
- **Contact** : Formulaire de contact stylé
- **Gymnase** : Informations sur le lieu d'entraînement
- **Licence** : Informations sur les licences
- **Réseaux sociaux** : Liens vers Instagram, Facebook, Twitter
- **Entraînement** : Tableau des créneaux d'entraînement
- **Gallery** : Galerie d'images du club

### Design System
- **Variables SCSS** centralisées
- **Composants réutilisables**
- **Responsive design** mobile-first
- **Animations fluides** et transitions modernes
- **Accessibilité** optimisée (navigation clavier, focus, aria-labels)
- **Glassmorphism** et effets visuels modernes

## 🎨 Personnalisation

### Couleurs
Modifiez les variables dans `assets/styles/base/_variables.scss` :
```scss
$primary-color: #2c3e50;
$secondary-color: #3498db;
$accent-color: #e74c3c;
```

### Ajouter un nouveau module
1. Créer le contrôleur dans `src/Controller/[Module]/`
2. Créer le template dans `templates/[module]/`
3. Ajouter la route dans le contrôleur
4. Mettre à jour la sidebar dans `templates/base.html.twig`
5. Ajouter la carte correspondante sur la page d'accueil

## 🧩 Structure des pages modulaires (Club, Équipes, Tournois...)

- **Titre et description** en haut de chaque page, centrés, sans margin-top, stylés via SCSS modulaire (ex : `.tournoi-page-title`, `.club-page-title`, `.team-page-title`)
- **Bouton d'action principal** (Créer une carte/équipe/tournoi) centré, gros, jaune, avec icône, visible uniquement pour les rôles autorisés (admin, président, super admin, etc.), stylé via `.admin-action-btn`
- **Bouton "Éditer"** bleu sur chaque carte, même style partout, visible pour les rôles autorisés
- **Aucun style inline dans les fichiers Twig** : tout le style est dans des fichiers SCSS modulaires dans `assets/styles/components/`
- **Droits d'accès** gérés dans le Twig avec `is_granted()`
- **Liens EasyAdmin** pour créer/éditer redirigent vers le CRUD correspondant avec le FQCN PHP (un seul antislash)

### Exemple d'ajout d'un nouveau menu (ex : "Partenaires")
1. Créer le contrôleur CRUD EasyAdmin (ex : `PartenaireCrudController.php`)
2. Créer le contrôleur public (ex : `PartenaireController.php`)
3. Créer le template Twig (ex : `templates/partenaire/index.html.twig`) avec :
   - Titre et description en haut
   - Bouton "Créer un partenaire" (admin-action-btn)
   - Boucle sur les partenaires avec bouton "Éditer" sur chaque carte
4. Créer un fichier SCSS modulaire (ex : `_partenaire-page.scss`) pour le style de la page
5. Importer ce SCSS dans `app.scss`
6. Ajouter le menu dans le Dashboard EasyAdmin avec les bons droits

**Cette structure permet d'ajouter/modifier n'importe quel menu très rapidement et de garder une cohérence visuelle et technique sur tout le projet.**

## 🔧 Configuration

### Webpack Encore
Le fichier `webpack.config.js` est configuré pour :
- Support SCSS
- Source maps en développement
- Hachage des fichiers en production
- Optimisation automatique

### Symfony
- Routing automatique avec annotations
- Templates Twig optimisés
- Cache configuré pour la production

## 📊 Performance

### Optimisations incluses
- **Lazy loading** des images
- **Minification** CSS/JS en production
- **Cache** Symfony optimisé
- **Compression** gzip
- **CDN ready** pour les assets
- **Pas de scroll horizontal** - layout parfaitement optimisé

## 🐛 Débogage

### Mode développement
```bash
# Activer le mode debug
APP_ENV=dev symfony server:start

# Voir les logs
tail -f var/log/dev.log
```

### Assets
```bash
# Recompiler les assets
npm run dev

# Voir les erreurs de compilation
npm run build
```

## 📝 Contribution

1. Fork le projet
2. Créer une branche feature (`git checkout -b feature/AmazingFeature`)
3. Commit les changements (`git commit -m 'Add some AmazingFeature'`)
4. Push vers la branche (`git push origin feature/AmazingFeature`)
5. Ouvrir une Pull Request

## 📄 Licence

Ce projet est sous licence MIT. Voir le fichier `LICENSE` pour plus de détails.

## 📞 Support

Pour toute question ou problème :
- Ouvrir une issue sur GitHub
- Contacter l'équipe de développement

---

**Badminton Agen** - Site web moderne et responsive pour le club de badminton d'Agen avec navigation sidebar intelligente et expérience utilisateur optimale. 
