# MS Custom — site vitrine

## Contenu du dossier

```
index.html      Le site complet (HTML + CSS + JS, un seul fichier)
merci.html      Page affichée après l'envoi du formulaire
netlify.toml    En-têtes de sécurité et cache
robots.txt      Instructions pour les moteurs de recherche
sitemap.xml     Plan du site pour Google
admin/          Panneau d'administration (ajout de réalisations sans code)
data/           realisations.json — le contenu de la galerie
assets/         Vos visuels, déjà intégrés :
                  hero.webp              visuel plein écran (Mercedes GLC)
                  logo.webp              logo néon (en-tête + pied de page)
                  favicon.png            icône d'onglet
                  apple-touch-icon.png   icône iPhone
                  og.jpg                 image de partage réseaux sociaux
                  galerie/*.webp         les 5 réalisations
```

## Mise en ligne sur Netlify

1. Placez ces fichiers dans un dossier.
2. Allez sur app.netlify.com → **Add new site** → **Deploy manually**.
3. Glissez le dossier dans la zone de dépôt. Le site est en ligne.
4. Les demandes de devis arrivent dans l'onglet **Forms** du site Netlify.
   Activez la notification par email dans *Forms → Settings → Form notifications*.

## Ce qu'il faut personnaliser avant la mise en ligne

| Où | Quoi |
|---|---|
| `<head>` | Remplacer `https://mscustom25.fr/` par votre vrai domaine (canonical, og:url, og:image, JSON-LD) |
| `robots.txt` et `sitemap.xml` | Y remplacer aussi `https://mscustom25.fr/` par votre domaine |
| Délai annoncé | Le site promet une réponse « sous 48 h » (hero, section devis, FAQ) — à ajuster si ce n'est pas votre rythme |
| Avis | 6 avis Google repris en abrégé, en prénom + initiale. À rafraîchir de temps en temps |

## Ajouter une réalisation depuis le panneau d'administration

Une fois la configuration faite (voir plus bas), rendez-vous sur **votre-domaine.fr/admin/**,
connectez-vous, ouvrez « Galerie des réalisations », cliquez sur **Ajouter réalisation**,
déposez la photo, remplissez les champs, puis **Publish**. Le site se met à jour tout seul
en une à deux minutes.

Recadrez la photo avant de la déposer (retirez l'interface Instagram) et exportez-la
en JPEG ou WebP de 1000 px de large environ.

### Configuration, à faire une seule fois

Le panneau a besoin que le site soit relié à un dépôt GitHub. C'est plus long que le
simple glisser-déposer, mais c'est ce qui permet ensuite de ne plus jamais toucher au code.

1. Créez un compte sur **github.com**, puis un dépôt (« repository ») nommé `ms-custom`.
2. Déposez-y tous les fichiers de ce dossier (bouton « uploading an existing file »).
3. Sur Netlify : **Add new site → Import an existing project → GitHub**, choisissez le dépôt.
4. Dans le site Netlify : **Integrations → Identity → Enable Identity**.
5. Toujours dans Identity : **Registration → Invite only** (personne d'autre ne pourra créer
   de compte), puis **Services → Git Gateway → Enable**.
6. **Identity → Invite users** : invitez votre adresse email. Vous recevez un lien,
   vous choisissez votre mot de passe, et vous arrivez sur le panneau.

À partir de là, tout passe par `/admin/`.

### Sécurité

`admin/` est exclu de Google (`robots.txt` et en-tête `X-Robots-Tag`), et l'inscription
est fermée : seules les personnes que vous invitez peuvent se connecter.

### Comment ça marche

La galerie du site lit `data/realisations.json`. Le panneau modifie ce fichier et envoie
les photos dans `assets/galerie/`. Les 16 réalisations actuelles restent aussi écrites en
dur dans `index.html` : elles servent de secours si le fichier de données est indisponible,
et permettent d'ouvrir le site en local par simple double-clic.

### Ajouter une réalisation sans le panneau

Si vous préférez rester en glisser-déposer, éditez directement `data/realisations.json` :
copiez un bloc existant, changez les valeurs, ajoutez la photo dans `assets/galerie/`.

## Après la mise en ligne : le référencement

Le site est prêt côté technique (titre, description, données structurées, plan du site).
Il reste deux gestes à faire une fois le domaine actif, et ils comptent autant que le code :

1. **Google Search Console** — ajoutez le site, puis envoyez `sitemap.xml`. C'est ce qui
   déclenche l'indexation en quelques jours au lieu de quelques semaines.
2. **Votre fiche Google Business** — ajoutez l'adresse du site dans la fiche. Le lien entre
   la fiche et le site est le premier facteur de référencement local, devant tout le reste.

Le site déclare déjà : vos horaires, votre téléphone, votre adresse, vos 4 prestations,
votre note de 5/5 sur 51 avis, et vos 6 questions fréquentes en données structurées
(Google peut les afficher directement dans les résultats de recherche).

## Modifier les tarifs

Les quatre packs sont écrits directement dans `index.html`, section `TARIFS`.
Cherchez `pack__prix` : le prix, le nom et le détail sont en clair, côte à côte.
Pensez à mettre à jour aussi le `minPrice` dans les données structurées, en haut du fichier.

## Modifier les couleurs

Tout est centralisé en haut du `<style>`, dans le bloc `:root`. Les accents sont calés sur les
couleurs relevées directement sur votre enseigne néon :

- `--bleu` `#2F8BFF` — le bleu du « MS »
- `--rose` `#E85CD2` — le rose du « CUSTOM »
- `--violet` `#7C4DE8` — la transition entre les deux
- `--noir` `#05070E` — un noir très légèrement bleuté, repris du fond du logo

Le dégradé `--seam` (le liseré lumineux qui traverse le site) découle de ces trois couleurs.

## Modifier les textes

Chaque section du HTML est précédée d'un commentaire en majuscules
(`PRESTATIONS`, `GALERIE`, `MÉTHODE`…). Le texte est en clair, sans framework.

## Ajouter une réalisation

Copiez un bloc `<article class="item">` dans la galerie, changez `data-marque`
(`mercedes`, `audi`, `bmw`, `porsche`, `volkswagen`, `autres`), le `src` de l'image,
le `alt`, la marque et le titre. Le filtre le prend en compte automatiquement.
