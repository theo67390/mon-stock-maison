# Mon Stock Maison — version avec partage familial

Cette version utilise Firebase Authentication (e-mail/mot de passe) et Realtime Database pour partager le stock entre plusieurs téléphones.

## Important
- Le fichier `index.html` contient la configuration Firebase Web du projet.
- Avant d'utiliser l'application, créez un utilisateur familial dans Firebase Authentication, activez le fournisseur E-mail/Mot de passe, puis configurez les règles Realtime Database pour autoriser **uniquement l'UID de cet utilisateur**.
- N'utilisez pas des règles publiques comme `.read: true` ou `.write: true`.
- L'accès commun signifie que chaque membre de la famille utilise le même e-mail et mot de passe. Partagez-les uniquement avec les personnes de confiance.
- La première connexion depuis un appareil dont le stock local contient déjà des produits peut importer ces produits si la base familiale est encore vide.
- Si des produits sont déjà présents dans la base, ils remplacent l'affichage local sur cet appareil.
- L'application n'inclut pas de création de compte publique.

## Configuration à effectuer dans Firebase
1. Authentication → Sign-in method → activer `Email/Password`.
2. Authentication → Users → Add user : créer un seul compte familial (e-mail + mot de passe).
3. Dans la liste Users, copier l'UID de cet utilisateur.
4. Realtime Database → Rules : remplacer les règles par le modèle ci-dessous en remplaçant `REMPLACER_PAR_UID` par l'UID réel :

```json
{
  "rules": {
    "familyStock": {
      ".read": "auth != null && auth.uid === 'REMPLACER_PAR_UID'",
      ".write": "auth != null && auth.uid === 'REMPLACER_PAR_UID'"
    }
  }
}
```

5. Cliquez sur Publish/Publier dans l'onglet Rules.
6. Remplacez les fichiers du dépôt GitHub par les fichiers de cette archive et validez les changements. GitHub Pages redéploiera l'application.
7. Connectez-vous sur chaque téléphone avec le même compte familial.

Ne passez pas à un forfait payant si vous souhaitez éviter les frais. Vérifiez que le projet et la base sont disponibles sur votre forfait actuel avant de continuer.


## Importer votre liste LibreOffice / OpenOffice
Une version préparée de votre liste est fournie en fichier `stock_maison_import.csv`. Dans Mon Stock Maison, connectez-vous au compte familial, puis utilisez « Importer une liste CSV ». L'import ajoute les produits au stock familial sans remplacer les produits déjà présents. Vérifiez les emplacements après import : « Congélateur cave » devient « Congélateur 1 », « Congélateur cuisine » devient « Congélateur 2 », et « Cave » devient « Autre ». Les dates de la colonne « Notes » sont conservées comme notes et ne sont pas converties en dates de péremption.

L'emplacement « Cave à vin » est également disponible dans le formulaire d'ajout et dans les filtres.

## Tableau, alertes et liste de courses
Cette version affiche l'inventaire sous forme de tableau, signale les produits dont la date de péremption est dépassée ou dans les 7 prochains jours, et ajoute une liste de courses partagée dans Firebase. La génération automatique de courses utilise les produits dont la quantité est inférieure au champ « Stock minimum » ; ce champ doit être renseigné dans les données des produits pour être utile. Les alertes sont visibles dans l'application (pas de notifications système automatiques).
