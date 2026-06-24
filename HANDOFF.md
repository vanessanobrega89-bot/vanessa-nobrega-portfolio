# HANDOFF — Projet Vanessa Nobrega (site + comm)

> Document de passation pour reprendre le projet (autre Claude / autre dev).
> À jour au dernier commit. **Ce fichier prime sur le `CLAUDE.md` d'origine**, qui décrit une ancienne direction visuelle (Bricolage Grotesque / prune) **abandonnée**.

---

## 1. Accès & démarrage rapide

- **Site en ligne** : https://vanessanobrega.com (apex uniquement, `www` ne résout pas)
- **Repo** : `https://github.com/vanessanobrega89-bot/vanessa-nobrega-portfolio.git` (branche `main`)
- **Hébergement** : Vercel (déploiement auto à chaque `git push origin main`)
- **Fichier principal du site** : `VNobrega-Landing-Salariat.html` (c'est LA landing servie à la racine, malgré son nom « Salariat »)
- **Contact** : vanessa.nobrega89@gmail.com · Nice / Cagnes-sur-Mer · LinkedIn `https://www.linkedin.com/in/vanessanobrega/`

### Déployer
`git add … && git commit && git push origin main` → Vercel build (~30-60 s). Vérifier en ligne avec `curl` + `?cb=$RANDOM` pour éviter le cache.

### Aperçu local (IMPORTANT : ~/Documents est bloqué par macOS TCC)
Le serveur d'aperçu sert depuis **`/tmp/vanessa-preview/`**, PAS depuis le dossier projet.
- On copie les fichiers modifiés dans `/tmp/vanessa-preview/` avant de prévisualiser.
- `.claude/launch.json` lance un `python3 -I -c` qui sert `/tmp/vanessa-preview` sur le port 8765.
- Le serveur python NE fait PAS les « clean URLs » → pour tester `/articles` en local, créer `articles/index.html` et `articles/<slug>/index.html` dans `/tmp`.

---

## 2. La personne & le positionnement

- **Vanessa Nobrega**, basée à Nice / Cagnes-sur-Mer. Sortie en mai 2026 de **5 ans à La Maison de l'IA** (acteur public-privé de référence sur l'IA en France).
- **Positionnement** : *Consultante Communication & IA* — « communication d'innovation ».
- **Tagline** : « J'accompagne votre communication à l'ère de l'IA. »
- **Double piste** : ouverte aux **missions freelance** ET aux **opportunités salariées** (postes com tech/IA). La comm de lancement doit rester ouverte aux deux.
- **3 spécialités** : (01) Communication & stratégie · (02) IA & vulgarisation · (03) Contenus & événementiel.

---

## 3. Charte visuelle (palette site)
```
--brown   #36291F   (fond foncé principal)
--beige   #ECE3D2   (fond clair)
--paper   #F7F1E4 / #FDFBF4
--ink     #2A2016 / #0A0A0A (texte foncé)
--accent / terracotta  #C16B3D   (orange-corail, accent signature)
--accent-deep  #A8511F
--line    #E8E5DC / #DDD2BD
--on-dark #EEE5D4 (crème, texte sur brun)
```
**Polices** : Cormorant Garamond (display/titres) · Inter (corps) · JetBrains Mono (labels/meta). Le **monogramme VN** est en **DM Serif Display** (favicon/OG).
Polices locales pour générer des visuels : `/tmp/ogfonts/` (cg.ttf, cg-it.ttf, inter.ttf, jbm.ttf) + `/tmp/dmserif.ttf`.

---

## 4. RÈGLES ÉDITORIALES — NON NÉGOCIABLES
- **Verbes prudents** pour les réalisations collectives : « contribué à », « animé », « accompagné », « co-organisé ». JAMAIS « créé/lancé seule » pour le **WAICF** (co-organisé avec Institut EuropIA, Ville de Cannes, Département 06).
- **Aucun chiffre inventé.** Seules preuves validées : 130 000+ personnes sensibilisées en 5 ans · 200+ événements/an · WAICF 10 000+ visiteurs pro (co-organisé) · ~20 partenaires · 5 ans à La Maison de l'IA.
- **Budget 200 K€/an : NE JAMAIS afficher** (interne, réservé aux CV/entretiens).
- **Pas de marque « Veoria »** (juste un email perso si besoin).
- **Tarifs** : toujours « sur devis selon périmètre », jamais de chiffres.
- **Préférence de Vanessa** : éviter les « tics de rédaction IA » (tirets cadratins à répétition, « Bonne nouvelle : », antithèses systématiques, aphorismes lisses). Ton incarné, 1ʳᵉ personne.

---

## 5. Architecture du site (`VNobrega-Landing-Salariat.html`, 1 seul fichier)
HTML + CSS inline + images en fichiers (dossier `photos-action/`, `logos/`). Pas de framework.

Ordre des sections (numérotées) :
1. Nav sticky (logo **VANESSA NOBREGA** en majuscules · liens Profil/Spécialités/Parcours/Formation/Journal · LinkedIn · CTA Contact). Nav **brune en haut**, **beige une fois scrollée**.
2. Hero (sec-brown) — tag « Consultante · Communication · IA » + titre « J'accompagne votre communication *à l'ère de l'IA.* » + accroche (texte **blanc** pour lisibilité, prévu pour un futur fond vidéo).
3. Marquee logos partenaires « Ils m'ont fait confiance ».
4. **01 Profil** (sec-beige) — photo `apropos-v5.jpg` (DSC_8948, plein cadre 2:3, sans filtre).
5. **02 Spécialités** (sec-beige) — 3 cartes (images spec-*).
6. **03 Outils** (sec-brown) — grille d'outils (icônes SVG base64), animée au scroll.
7. **04 Parcours** (sec-brown) — expériences ; logos entreprises blanchis (`filter invert`).
8. **05 Formation & Langues** (sec-beige).
9. **06 Journal** (sec-beige) — aperçu des 3 articles (vignettes photo N&B), lien « Voir tous les articles ».
10. **07 Contact** (sec-brown) — formulaire FormSubmit + LinkedIn.
11. Bandeau « En action » (carrousel photos, animation `ps-scroll`).
12. Footer (sec-brown) — liens + « Mentions légales & confidentialité » + « En partenariat avec Troie Studio ».

**Animations au scroll** (IntersectionObserver, init **après `window.load`** pour éviter le déclenchement prématuré dû aux images lazy) : Spécialités (cascade + zoom), Outils (colonnes), Formation (lignes), Parcours (glissé latéral `exp-slide`). Respect de `prefers-reduced-motion`.

---

## 6. Ce qui a été construit / livré
- **SEO/partage** : `<title>`, meta description, **OG = `og-image-v9.png`** (photo tabouret + « VANESSA NOBREGA » DM Serif), Twitter card, **schema.org Person** (landing) + **Article** (chaque article).
- **Favicon / apple-touch-icon** : monogramme VN **vectorisé en DM Serif Display** (`favicon.svg`, `apple-touch-icon.png`). Cache-bust via `?v=2`.
- **Mentions légales & confidentialité** : `mentions-legales.html` → `/mentions-legales` (RGPD : formulaire, FormSubmit, Google Fonts, Vercel Analytics ; sans SIRET, à compléter à l'immatriculation).
- **Analytics** : **Vercel Web Analytics** (script `/_vercel/insights/script.js`, sans cookie) + **2 events** : `contact_envoi` (submit formulaire) et `clic_linkedin`. ⚠️ À **activer dans le dashboard Vercel** (onglet Analytics → Enable) pour que ça collecte.
- **Blog « Journal »** : `articles.html` → `/articles` + 3 articles evergreen dans `articles/` :
  - `parler-ia-sans-jargon` (IA & Vulgarisation)
  - `communication-innovation-par-ou-commencer` (Communication d'innovation)
  - `ia-communication-sans-perdre-incarnation` (IA & Contenus)
  - Vignettes = photos N&B (stock-salon-v2 / art-innovation2 / art-contenus). Couvertures typo « Clair./Désirable./Augmentée. » gardées **en réserve** (`art-cover-*.jpg`).
- **Partenariat Troie Studio** : mention footer + tournure « Pour les projets d'envergure, je m'associe à l'agence Troie Studio ».

---

## 7. Déploiement, aperçu & pièges connus
- **`.gitignore`** ignore TOUTES les images (`*.jpg/png/webp`) puis **allowlist** explicite (`!photos-action/xxx.jpg`). **Toute nouvelle image doit être ajoutée à l'allowlist**, sinon `git add` la skippe → 404 en prod. Vérifier avec `git status` (ligne `A`).
- **Cache navigateur** : pour un changement de contenu d'image, utiliser un **nouveau nom de fichier** (ex. `og-image-v9` plutôt qu'écraser `v8`).
- **`git rm <img>` puis `git add … <même img>`** casse le staging (pathspec disparu) → ne re-lister jamais le fichier supprimé. Vérifier avec `git show --stat HEAD`.
- **Clean URLs** : Vercel (`cleanUrls:true`) sert `/articles` depuis `articles.html` et `/articles/<slug>` depuis `articles/<slug>.html`. Le serveur python local NE le fait pas (voir §1).
- **OG sur réseaux** : purger le cache via LinkedIn Post Inspector / Facebook Sharing Debugger après chaque changement d'OG.

---

## 8. État actuel & à faire (pending)
- [ ] **Activer Vercel Web Analytics** dans le dashboard (sinon 0 donnée).
- [ ] **Activer FormSubmit** : faire un 1er envoi test depuis le formulaire + cliquer le mail de confirmation.
- [ ] **Mentions légales** : ajouter le **SIRET** + forme juridique dès l'immatriculation (commentaire `<!-- À COMPLÉTER -->` dans `mentions-legales.html`).
- [ ] **Images du Journal** : Vanessa remplacera peut-être les vignettes par d'autres images plus tard.
- [ ] **Logo pages articles** : laissé en « VN » (la landing est en « VANESSA NOBREGA »). À harmoniser si souhaité.
- [ ] **Fond vidéo hero** : envisagé (l'accroche est déjà en blanc) ; prévoir un voile sombre + fallback image + pause `prefers-reduced-motion`.

---

## 9. Assets externes (hors repo, dans ~/Downloads)
- `VN-stories/` — stories de lancement Vanessa (1080×1920)
- `VN-photos-site/` — photos du site avec filtres « cuits »
- `VN-banniere-linkedin.png` — bannière LinkedIn 1584×396
- `Troie-stories/` — 7 stories pour Troie Studio (charte orange)
- OG / bannières diverses : `og-image-v*.png`, `banniere-*.png`, etc. (dans le repo à la racine)

---

## 10. Comm de lancement (prête)
- **Post LinkedIn (long)** et **caption Instagram** rédigés (ton perso pour l'Insta). Structure : « ✦ Nouveau chapitre » → activité → 3 spécialités → « 🤎 Pour les projets d'envergure je m'associe à Troie Studio » → lien.
- **Lien dans le post** (recommandé) plutôt qu'en commentaire.
- **Timing optimal (France/CET)** : LinkedIn mar/mer/jeu **8h30** · Instagram mar→ven **12h-13h** ou **18h-20h** · Stories le soir 19h-21h.
- Emoji « charte » validés : ✦ ▪️ 🤎 → (éviter 🚀✨🔥).

---

## 11. Troie Studio (partenaire)
- Site : https://troiestudio.fr/fr — « Un studio. Trois métiers » : Création / Stratégie / Formation IA. Ton direct, sans jargon. (10 ans, 50 entreprises, 200 pros formés — **à faire valider par eux** avant réutilisation).
- **Charte Troie** : orange `#F37B22`, brun `#1A1714`, crème `#F5F0E6`. Police visuels : Space Grotesk + JetBrains Mono.
- Texte de présentation (voix agence) et 7 stories déjà produits.
```
```
