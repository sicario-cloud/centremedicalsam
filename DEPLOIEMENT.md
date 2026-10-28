# Mise en ligne — centremedicalsam.com

Site statique (HTML/CSS, aucun serveur ni base de données). Hébergement gratuit recommandé : **GitHub Pages**. Alternative sans ligne de commande : **Netlify** (option B).

## Contenu du dossier

| Fichier | Rôle |
|---|---|
| `index.html` | La page complète (styles et script intégrés) |
| `assets/` | Logo, icônes, image de partage (Open Graph) |
| `favicon.ico`, `site.webmanifest` | Icônes du navigateur |
| `robots.txt`, `sitemap.xml` | Référencement (SEO) |
| `CNAME`, `.nojekyll` | Configuration GitHub Pages |

Pour prévisualiser localement : ouvrir `index.html` dans un navigateur.

---

## Option A — GitHub Pages (gratuit, recommandé)

### 1. Publier le site sur GitHub
1. Créer un compte sur <https://github.com> (gratuit).
2. Cliquer **New repository** → nom : `centremedicalsam` → **Public** → **Create repository**.
3. Cliquer **uploading an existing file**, glisser **tout le contenu** du dossier (y compris `assets/`, `CNAME` et `.nojekyll`), puis **Commit changes**.
   - Sur Mac, les fichiers commençant par un point sont masqués : dans le Finder, appuyer sur `Cmd + Shift + .` pour les afficher.
4. Aller dans **Settings → Pages** :
   - *Source* : **Deploy from a branch** → branche `main`, dossier `/ (root)` → **Save**.
   - *Custom domain* : `centremedicalsam.com` → **Save**.

### 2. Configurer le DNS chez Namecheap
1. Namecheap → **Domain List** → **Manage** à côté de `centremedicalsam.com`.
2. Onglet **Domain** → *Nameservers* : **Namecheap BasicDNS**.
3. Onglet **Advanced DNS** → supprimer les enregistrements par défaut de type *URL Redirect* et *CNAME* `www` → `parkingpage.namecheap.com`.
4. Ajouter :

| Type | Host | Value | TTL |
|---|---|---|---|
| A Record | `@` | `185.199.108.153` | Automatic |
| A Record | `@` | `185.199.109.153` | Automatic |
| A Record | `@` | `185.199.110.153` | Automatic |
| A Record | `@` | `185.199.111.153` | Automatic |
| CNAME Record | `www` | `VOTRE-NOM-UTILISATEUR.github.io.` | Automatic |

(Remplacer `VOTRE-NOM-UTILISATEUR` par votre nom d’utilisateur GitHub.)

### 3. Activer le HTTPS
Après la propagation DNS (de quelques minutes à 24 h), retourner dans **Settings → Pages** et cocher **Enforce HTTPS**.
Si la case est grisée, attendre encore un peu : GitHub génère le certificat automatiquement.

### Mettre à jour le site
Modifier `index.html`, puis dans le dépôt GitHub : **Add file → Upload files** (remplacer le fichier). La mise à jour est en ligne en 1 à 2 minutes.

---

## Option B — Netlify (glisser-déposer)

1. Créer un compte gratuit sur <https://app.netlify.com>.
2. **Add new site → Deploy manually** → glisser le dossier complet du site.
3. **Domain management → Add a domain** → `centremedicalsam.com`.
4. Chez Namecheap, **Advanced DNS** (supprimer les enregistrements de parking, puis ajouter) :

| Type | Host | Value |
|---|---|---|
| A Record | `@` | `75.2.60.5` |
| CNAME Record | `www` | `NOM-DU-SITE.netlify.app.` |

5. Netlify active le HTTPS automatiquement (Let’s Encrypt) après la vérification du DNS.
6. Le fichier `CNAME` est ignoré par Netlify ; il peut rester dans le dossier.

---

## Courriels (@centremedicalsam.com)

Le site affiche `administration@` et `direction@centremedicalsam.com`. Ces adresses doivent exister pour recevoir les messages :
- **Namecheap Private Email**, **Google Workspace** ou **Zoho Mail**, ou
- **Namecheap Email Forwarding** (gratuit, redirige vers une boîte existante) : *Domain → Redirect Email*.

Les enregistrements **MX** et **TXT** du service de courriel s’ajoutent dans *Advanced DNS* ; ils n’entrent pas en conflit avec les enregistrements A/CNAME du site.

---

## Après la mise en ligne

- Vérifier : <https://centremedicalsam.com> et <https://www.centremedicalsam.com> (doit rediriger vers la version sans `www`).
- Inscrire le site à **Google Search Console** et soumettre `https://centremedicalsam.com/sitemap.xml`.
- Tester l’aperçu de partage : <https://www.opengraph.xyz>.
- À l’ouverture : retirer les mentions « Ouverture prochaine » et les étiquettes « Prévu » dans `index.html`, et passer `isAcceptingNewPatients` à `true` dans le bloc JSON-LD.
