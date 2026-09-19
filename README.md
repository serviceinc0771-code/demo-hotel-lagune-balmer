# Hôtel Lagune Balmer — template Astro + Tailwind

Site vitrine **démo** pour un hôtel fictif à **San-Pédro** (Côte d’Ivoire). Interface en français, réservation via **WhatsApp** uniquement (pas de moteur de booking, paiement, auth ni CMS).

Design **premium San-Pédro** : océan / lagune / écume / terre cuite. Quatre pages. Tarifs depuis `hotel.json`.

## Stack

- [Astro](https://astro.build) + [Tailwind CSS v4](https://tailwindcss.com) (`@tailwindcss/vite`)
- Typo : **Fraunces** + **Playfair Display** (titres), **DM Sans** (texte) via Google Fonts
- Prêt pour **Vercel** (`npm run build` → `dist/`)

## Design tokens

| Token | Hex | Usage |
| --- | --- | --- |
| `--ocean` | `#0B1C24` | Hero, header solide, footer |
| `--lagoon` | `#0F3D3E` | Bandeau confiance, accents, prix |
| `--foam` | `#F4EDE3` | Cartes, texte sur fond sombre |
| `--sand` | `#EADDC8` | Fond des pages |
| `--terracotta` | `#C8613F` | CTA WhatsApp (hover `#A84E32`) |
| `--border` | `#D9CBB6` | Filets des cartes |

Mouvement : reveal au scroll (fade + 12px, `IntersectionObserver`) ; Ken Burns CSS sur le still **mobile** uniquement. `prefers-reduced-motion` désactive les animations.

## Installation

```bash
cd hotel-lagune-balmer
npm install
```

## Développement

```bash
npm run dev
```

Ouvre typiquement `http://localhost:4321`.

## Build & prévisualisation

```bash
npm run build
npm run preview
```

## Personnaliser le contenu (`src/data/hotel.json`)

**Un seul fichier de contenu :** `src/data/hotel.json` (utilisé partout).

| Champ | Rôle |
| --- | --- |
| `name`, `tagline`, `city`, `address` | Identité & localisation |
| `phone` / `phoneDisplay`, `whatsapp`, `email` | Contact (`whatsapp` = chiffres sans `+`, ex. `2250700000000`) |
| `whatsappPrefill` | Message général (bouton flottant, footer, contact) |
| `rooms[]` | Chambres (`id`, `name`, `price`, `currency`, `capacity`, `description`, `image`, `amenities`, **`whatsappPrefill`** par chambre) |
| `amenities`, `practical` | Services & infos pratiques |
| `demoNotice` | Bannière « établissement fictif » |

Tarifs démo : Standard **25 000** / Confort **40 000** / Famille **55 000** FCFA.

Après modification : relancer `npm run dev` ou `npm run build`.

### Prefill WhatsApp par chambre

Chaque chambre a son `whatsappPrefill`. Les CTA de `RoomCard` ouvrent :

`https://wa.me/${whatsapp}?text=${encodeURIComponent(message)}`

Le formulaire (`ReservationForm`) assemble nom / dates / chambre **côté navigateur** puis ouvre WhatsApp — aucun backend.

## Images & vidéo hero

Fichiers locaux dans `public/images/` :

- `hero.jpg` — still tropical lagune/plage (Unsplash), **toujours** utilisé comme poster
- `place.jpg` — still plage (bloc « le lieu »)
- `chambre-standard.jpg`, `chambre-confort.jpg`, `chambre-famille.jpg`

**Vidéo :** aucun fichier beach/lagune assez léger n’était disponible. Le hero desktop reste donc le still Unsplash (sans Ken Burns). Pour activer une vidéo muette en boucle **md+ uniquement**, placez un MP4 compressé ici :

`public/videos/hero.mp4`

`Hero.astro` le détecte au build (`poster` = `hero.jpg`). Mobile : still + Ken Burns CSS, **pas** de vidéo lourde. `prefers-reduced-motion` = image fixe, pas d’autoplay.

Sources Unsplash (à remplacer par des photos de l’établissement réel, puis compresser ~100–300 Ko) :

- Hero : [photo-1559827260-dc66d52bef19](https://unsplash.com/photos/1559827260-dc66d52bef19)
- Place : [photo-1507525428034-b723cf961d3e](https://unsplash.com/photos/1507525428034-b723cf961d3e)

Chemins chambres dans `hotel.json` → `rooms[].image`.

## Déploiement Vercel

1. Importez le dépôt sur [Vercel](https://vercel.com).
2. Framework : Astro · Build : `npm run build` · Output : `dist`.

```bash
npx vercel
```

## Structure

```text
hotel-lagune-balmer/
  package.json
  astro.config.mjs
  tsconfig.json
  public/images/
  src/data/hotel.json
  src/layouts/BaseLayout.astro
  src/components/
    Header.astro, Footer.astro, Hero.astro,
    RoomCard.astro, WhatsAppButton.astro, ReservationForm.astro
  src/pages/
    index.astro      → Accueil
    chambres.astro   → Chambres
    infos.astro      → Infos
    contact.astro    → Contact
  src/styles/global.css
  README.md
```

## Hors scope

- Moteur de réservation / calendrier
- Paiement en ligne
- Auth / CMS
- Routes dynamiques `chambres/[slug]`
- React (sauf le petit script client du formulaire WhatsApp)

## Démo

Établissement **fictif**. Remplacez textes, tarifs, numéro WhatsApp et images avant une mise en production réelle. Le footer affiche **DÉMONSTRATION — établissement fictif**.
