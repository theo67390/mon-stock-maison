# Mon Stock Maison — démarrage

## Ce que fait cette version
- Inventaire des placards, du réfrigérateur et de deux congélateurs (plus un emplacement « Autre »).
- Quantités et unités, dates limites, recherche et filtres.
- Ajout, retrait et suppression des produits.
- Lecture caméra des codes-barres sur les navigateurs Android compatibles. La recherche Open Food Facts peut remplir le nom lorsqu'il existe dans la base.
- Export/import d'une sauvegarde JSON.
- Interface installable comme application web (PWA) lorsqu'elle est hébergée en HTTPS.

## Important
Les données sont stockées localement sur le navigateur de chaque téléphone. **La synchronisation familiale entre plusieurs téléphones n'est pas encore activée** dans cette version. Pour avoir un inventaire partagé en direct, il faut ajouter une base cloud (par exemple Firebase), configurer l'accès familial et publier le site en HTTPS. Ne mettez pas de données privées dans une base cloud non sécurisée.

## Installer sur Android pour tester
1. Publier le dossier sur un hébergement HTTPS (par exemple un hébergement statique).
2. Ouvrir l'adresse du site dans Chrome sur Android.
3. Menu ⋮ → « Ajouter à l'écran d'accueil » ou « Installer l'application ».
4. Autoriser la caméra quand le navigateur le demande pour scanner les codes-barres.

Le scan caméra et le service worker exigent généralement un contexte sécurisé HTTPS (ou localhost). La compatibilité de BarcodeDetector dépend du navigateur. La saisie manuelle du code-barres reste possible.

## Fichiers
- `index.html` : interface et logique
- `manifest.json` : paramètres d'installation
- `sw.js` : cache hors ligne de base
- `icon.svg` : icône
