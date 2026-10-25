# E&G — Boutique en ligne

Site vitrine de la boutique **E&G** (bijoux, chaussures, parfums et accessoires — Abomey-Calavi, Bénin).
Les commandes passent par WhatsApp, le catalogue est stocké dans **Firebase Firestore**.

## Fichiers

| Fichier | Rôle |
|---|---|
| `index.html` | Tout le site (HTML, CSS et JavaScript) |
| `firestore.rules` | Règles de sécurité à copier dans la console Firebase |
| `favicon.svg`, `apple-touch-icon.png` | Icônes de l'onglet et de l'écran d'accueil |
| `og-image.jpg` | Image d'aperçu quand le lien est partagé (WhatsApp, Facebook…) |

## Fonctionnalités

- Catalogue avec filtres par catégorie et recherche
- Jusqu'à 3 photos par article, fiche détaillée avec galerie
- Lien direct vers un article (`…/#article-ID`) et bouton « Partager »
- Panier : toute la sélection est envoyée en **un seul message WhatsApp**
- Tailles / pointures et statut « en stock / épuisé » par article
- Espace admin (ajout, modification, suppression) protégé par Firebase Authentication

## Données Firestore

- `produits/{id}` : nom, prix, catégorie, description, tailles, disponibilité, **miniatures** (légères)
- `produitsPhotos/{id}` : photos en grande taille, chargées seulement quand on ouvre la fiche

## Mise en place de la sécurité (à faire une fois)

1. Console Firebase → **Authentication** → Commencer → activer **E-mail/Mot de passe**.
2. Onglet **Users** → **Ajouter un utilisateur** (ton email + un mot de passe solide).
3. Copier l'**UID** de cet utilisateur.
4. **Firestore Database** → **Règles** : coller le contenu de `firestore.rules`,
   vérifier que l'UID est bien celui du compte admin, puis **Publier**.
5. Sur le site : bouton **Admin** → se connecter avec cet email.
6. Si une barre « anciens articles » apparaît, cliquer sur **Optimiser maintenant**.

> La configuration Firebase visible dans `index.html` est publique par nature : ce n'est pas un secret.
> Ce sont les règles Firestore qui empêchent les visiteurs de modifier le catalogue.
