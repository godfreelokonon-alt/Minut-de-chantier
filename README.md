# Minuté de chantier

Application web de suivi horaire des opérations sur chantier ferroviaire (ITC).
Conçue pour remplacer la feuille et le stylo par un outil numérique simple,
utilisable sur téléphone depuis le terrain — y compris en tunnel.

![Aperçu de l'application](docs/apercu.png)

## Aperçu

Un seul fichier HTML, zéro installation, zéro dépendance backend. Le chef de
chantier prépare la liste des tâches au bureau et la partage à son équipe par
QR code. Sur le terrain, chaque équipier horodate les opérations d'un clic.
En fin d'ITC, un rapport PDF professionnel est généré en un clic.

## Fonctionnalités

- **Horodatage au clic** — bouton "Démarrer" et "Terminer" pour chaque tâche,
  l'heure système est prise automatiquement
- **Correction rétroactive** — tap sur une heure pour la modifier si on a oublié
- **Bouton incident** accessible en permanence, section dédiée dans le rapport
- **Partage du plan par QR code** — le chef scanne, l'équipe récupère la fiche
  pré-remplie
- **Gestion des ITC de nuit** — détection automatique de la traversée de minuit
- **Réorganisation des tâches par glisser-déposer** (souris et tactile)
- **Sauvegarde automatique** dans le navigateur + export/import JSON pour
  archivage qualité
- **Export PDF** avec en-tête chantier, tableau des opérations, incidents et
  cases signature
- **Fonctionne hors ligne** une fois la page chargée (utile en tunnel)
- **Interface responsive** — testée sur mobile portrait dès 360px de large

## Démo

L'application est hébergée sur GitHub Pages :

[https://votre-username.github.io/minute-de-chantier/](https://votre-username.github.io/minute-de-chantier/)

## Utilisation

### Ouvrir l'application

Ouvrir l'URL ci-dessus dans un navigateur récent (Chrome, Safari, Firefox,
Edge). Aucune installation.

Sur mobile, vous pouvez ajouter la page à l'écran d'accueil pour un accès
type application native :
- **iPhone** : bouton Partager → "Sur l'écran d'accueil"
- **Android** : menu → "Ajouter à l'écran d'accueil"

### Préparer un chantier au bureau

1. Remplir l'en-tête (nom, n° ITC, lieu, responsable, date)
2. Ajouter les tâches prévues via le bouton "Ajouter une tâche"
3. Réordonner si besoin en glissant la poignée à gauche
4. Cliquer sur "Partager" pour obtenir un QR code ou un lien à transmettre
   à l'équipe

### Sur chantier

Pour chaque opération :
- Bouton **Démarrer** → l'heure de début est enregistrée
- Bouton **Terminer** → l'heure de fin est enregistrée, la durée est calculée
- Bouton **+ suivante** → termine l'opération en cours et démarre la suivante
- Champ commentaire sous la tâche pour les observations

Si on a oublié un horodatage : taper sur l'heure affichée pour la modifier.

En cas d'incident : bouton rouge en haut à droite, description, validation.

### En fin d'ITC

- Bouton **PDF** → génère un rapport professionnel via le dialogue d'impression
  du navigateur (choisir "Enregistrer en PDF")
- Bouton **Exporter** → télécharge un fichier JSON à archiver dans le dossier
  qualité du chantier

## Déploiement

### GitHub Pages (recommandé)

1. Cloner ou télécharger ce dépôt
2. Pousser le fichier `minute-de-chantier.html` à la racine de votre propre repo
3. Activer GitHub Pages dans `Settings` → `Pages` → source `main` branch
4. L'URL publique sera du type `https://<votre-user>.github.io/<votre-repo>/minute-de-chantier.html`

### Hébergement local ou intranet

Le fichier `minute-de-chantier.html` est autonome. Il suffit de le déposer sur
n'importe quel serveur web (Apache, Nginx, IIS) ou même de l'ouvrir en local
(`file://`). Attention : la fonction QR code nécessite un accès Internet au
premier chargement pour mettre en cache la librairie externe.

## Architecture technique

- **HTML/CSS/JavaScript vanilla** — aucun framework
- **Single-file** — tout le code (HTML, CSS, JS) dans un seul fichier
- **Stockage** — `localStorage` pour la persistance locale, export/import JSON
  pour l'archivage
- **QR code** — [qrcode-generator](https://github.com/kazuhikoarase/qrcode-generator)
  v1.4.4 (domaine public), chargé via CDN jsDelivr
- **Polices** — polices système (`-apple-system`, `Inter`, `Segoe UI`) — aucune
  police externe à charger
- **Impression** — CSS `@media print` dédié pour un rendu PDF propre

## Compatibilité navigateurs

Testé et fonctionnel sur :
- Safari iOS 15+
- Chrome Android 100+
- Chrome desktop 100+
- Firefox desktop 100+
- Edge 100+

## Limites connues

- La fonctionnalité QR code nécessite un accès Internet au premier chargement.
  Une fois la librairie mise en cache, elle fonctionne hors ligne.
- Les données sont stockées dans le navigateur (localStorage). En navigation
  privée sur iPhone, la sauvegarde automatique peut être désactivée — l'app
  affiche un avertissement le cas échéant.
- L'application n'est pas collaborative en temps réel. Chaque équipier remplit
  sa propre fiche. Un rapport consolidé doit être produit par un reporter désigné.

## Roadmap

Améliorations envisagées :

- [ ] Mode PWA (Progressive Web App) pour installation native et cache offline
      complet dès le premier accès
- [ ] Export CSV en complément du PDF pour exploitation dans Excel
- [ ] Horodatage live visible ("démarrée il y a 12 min")
- [ ] Undo après suppression d'une tâche
- [ ] Modèles de chantier réutilisables (bibliothèque de tâches-types)

## Contribution

Les remontées terrain sont les bienvenues. Ouvrir une issue pour signaler un
bug ou suggérer une amélioration, en précisant :
- Le navigateur et la version utilisés
- Le contexte (préparation bureau / utilisation terrain / fin d'ITC)
- Les étapes pour reproduire si c'est un bug

## Licence

MIT — voir `LICENSE`.

## Auteur

Développé pour un usage interne Ingénierie voie, à la suite d'une nuit de
chantier RVB sur le RER A où le besoin s'est fait sentir.
