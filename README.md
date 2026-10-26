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

**Côté visiteur**
- Catalogue avec filtres par catégorie et recherche (3 articles par ligne sur téléphone)
- Jusqu'à 3 photos par article, fiche détaillée avec galerie et **zoom** (double appui, pincer)
- **Vous aimerez aussi** : 4 suggestions en bas de chaque fiche
- **Favoris ♥** gardés sur le téléphone du visiteur, avec un filtre dédié
- Article épuisé : bouton **Me prévenir** (message WhatsApp prêt à envoyer)
- Panier : toute la sélection est envoyée en **un seul message WhatsApp**
- Lien direct vers un article (`…/#article-ID`) et bouton « Partager »
- **Mode sombre / clair** : suit le réglage du téléphone, ou le bouton ☾ / ☀

**Côté admin** (lien « Espace admin » en bas de page, ou `…/#admin`)
- Barre admin dédiée : ＋ Article · 📢 Bandeau · 📊 Statistiques · Quitter
- En mode admin, les boutons d'achat sont cachés : chaque carte affiche ses compteurs et « Modifier / Supprimer »
- **Bandeau défilant** : messages définis par l'admin ; vide = aucun bandeau
- **Statistiques** par article : 👁 vues (fiches ouvertes) et 📦 commandes (clics « Commander »)
  (les visites de l'admin ne sont pas comptées)

## Données Firestore

- `produits/{id}` : nom, prix, catégorie, description, tailles, disponibilité, **miniatures** (légères)
- `produitsPhotos/{id}` : photos en grande taille, chargées seulement quand on ouvre la fiche
- `config/site` : réglages du site (messages du bandeau défilant)
- `stats/{id}` : compteurs par article (`views`, `orders`) — les visiteurs ne peuvent qu'ajouter +1
  (les règles acceptent encore `cart`, un ancien compteur qui n'est plus utilisé)

## Mise en place de la sécurité (à faire une fois)

1. Console Firebase → **Authentication** → Commencer → activer **E-mail/Mot de passe**.
2. Onglet **Users** → **Ajouter un utilisateur** (ton email + un mot de passe solide).
3. Copier l'**UID** de cet utilisateur.
4. **Firestore Database** → **Règles** : coller le contenu de `firestore.rules`,
   vérifier que l'UID est bien celui du compte admin, puis **Publier**.
5. Sur le site : lien **Espace admin** en bas de page (ou `…/#admin`) → se connecter avec cet email.
6. Si une barre « anciens articles » apparaît, cliquer sur **Optimiser maintenant**.

> La configuration Firebase visible dans `index.html` est publique par nature : ce n'est pas un secret.
> Ce sont les règles Firestore qui empêchent les visiteurs de modifier le catalogue.
