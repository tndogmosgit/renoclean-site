# Design doc — Améliorations V2 site RENOCLEAN

## Contexte

Amélioration complète du site vitrine RENOCLEAN existant sur 3 axes : contenu, design visuel, fonctionnalités + SEO. Le site est déjà en ligne sur `renoclean-site.vercel.app`.

---

## 1. Contenu

### Informations réelles à intégrer
- Téléphone : `06 05 58 70 97` (lien `tel:+33605587097`)
- Localisation : Rueil-Malmaison (92)
- Zone d'intervention : toute l'Île-de-France (75, 77, 78, 91, 92, 93, 94, 95)
- Email : `contact@renoclean.fr`

### Page d'accueil
- Hero badge : "Basé à Rueil-Malmaison · Intervention IDF"
- Bouton téléphone dans la nav (desktop) + en bas du menu mobile
- Section "Ils nous font confiance" → texte sobre sans faux témoignages : *"Vous êtes parmi nos premiers clients — partagez votre expérience"* + bouton Google Avis (lien placeholder)
- Bouton WhatsApp flottant bas-droite sur toutes les pages

### Page nettoyage diogène
- FAQ enrichie avec mots-clés locaux (Rueil-Malmaison, Île-de-France, 92, nettoyage diogène)
- Section zones d'intervention : liste des départements IDF couverts

### Page à propos
- Adresse : Rueil-Malmaison (92)
- Téléphone : 06 05 58 70 97
- Email : contact@renoclean.fr

### Page devis
- Encart au-dessus du formulaire : *"Besoin d'une réponse rapide ? Appelez-nous : 06 05 58 70 97"*

---

## 2. Design visuel

### Animations
- Entrée en fondu des sections au scroll via `IntersectionObserver` (JS vanilla, 0 dépendance)
- Cards hover : `translateY(-4px)` + ombre accentuée
- Bouton CTA principal : animation pulse subtile (CSS keyframes)
- Nav : ombre portée apparaît au scroll (`scroll` event listener)

### Images & icônes
- Emojis remplacés par icônes SVG inline (propres, accessibles, pas de dépendance)
- Photo hero : image Unsplash libre de droits (appartement propre) en overlay semi-transparent sur le gradient
- Galerie avant/après : section HTML préparée avec placeholders visuels, cachée avec classe `.hidden` (activable plus tard)

### Effets premium
- Séparateur vague SVG entre le hero et la section split
- Section stats : compteur animé au scroll (0 → valeur finale)

---

## 3. Fonctionnalités

### Téléphone
- Nav desktop : bouton `<a href="tel:+33605587097">` à côté du CTA devis
- Menu mobile : numéro affiché en bas du menu déroulant
- Page devis : encart cliquable au-dessus du formulaire

### WhatsApp flottant
- Bouton fixe bas-droite sur toutes les pages
- Lien : `https://wa.me/33605587097?text=Bonjour%2C%20je%20souhaite%20un%20devis%20pour%20un%20nettoyage%20diog%C3%A8ne`
- Icône SVG WhatsApp + label "Nous écrire"
- Visible sur mobile et desktop

---

## 4. SEO technique

### Balises meta enrichies (toutes les pages)
- `<title>` et `<meta name="description">` avec mots-clés locaux (Rueil-Malmaison, IDF, nettoyage diogène)
- `<meta name="keywords">` sur chaque page
- `<link rel="canonical">` pointant vers l'URL Vercel

### Schema.org LocalBusiness (index.html uniquement)
```json
{
  "@context": "https://schema.org",
  "@type": "LocalBusiness",
  "name": "RENOCLEAN",
  "telephone": "+33605587097",
  "email": "contact@renoclean.fr",
  "address": {
    "@type": "PostalAddress",
    "addressLocality": "Rueil-Malmaison",
    "postalCode": "92500",
    "addressCountry": "FR"
  },
  "areaServed": "Île-de-France",
  "url": "https://renoclean-site.vercel.app"
}
```

### Fichiers techniques
- `sitemap.xml` : liste statique des 5 pages avec `<lastmod>` et `<priority>`
- `robots.txt` : `Allow: /`, `Sitemap:` pointant vers sitemap.xml

### Préparation pub
- `<meta name="google-site-verification" content="A_REMPLIR">` dans le `<head>` de toutes les pages
- Commentaire placeholder Pixel Meta dans le `<head>` de toutes les pages

---

## Fichiers modifiés

| Fichier | Changements |
|---|---|
| `index.html` | Tel nav, hero badge, section témoignages, WhatsApp, schema.org, meta SEO, animations |
| `nettoyage-diogene.html` | FAQ enrichie, zones IDF, meta SEO, WhatsApp |
| `renovation.html` | Meta SEO, WhatsApp |
| `a-propos.html` | Adresse, tel, email, meta SEO, WhatsApp |
| `devis.html` | Encart tel, meta SEO, WhatsApp |
| `css/style.css` | Animations, pulse CTA, nav shadow, wave SVG, WhatsApp flottant, galerie hidden |
| `js/main.js` | IntersectionObserver, nav shadow scroll, compteur stats |
| `sitemap.xml` | Nouveau fichier |
| `robots.txt` | Nouveau fichier |

## Hors scope V2
- Galerie avant/après avec vraies photos (préparée mais cachée)
- Google Avis (lien placeholder)
- Pixel Meta (commentaire placeholder)
- Email pro contact@renoclean.fr (lié au nom de domaine)
