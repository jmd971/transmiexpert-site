# CLAUDE.md — TransmiExpert (site)

Mémoire projet pour Claude Code. À lire à chaque session avant toute modification.

---

## 1. Stack technique

- Site HTML statique pur. Aucun framework, aucun build, aucune compilation.
- Déploiement : Vercel, automatique à chaque push sur `main`. Config : `vercel.json`.
- 100 % HTML. Le CSS est embarqué INLINE dans des balises `<style>` à l'intérieur
  de chaque page. Il n'existe PAS de feuille de style externe partagée. ✅ Confirmé.
- Les fichiers sont LOURDS mais les images base64 ont été externalisées (voir §8).
  Ne jamais charger une page entière sans raison : cibler par grep.

### Conséquences directes (règles d'édition)
- Toute modification de style ou de structure de bloc est LOCALE à une page.
  Elle ne se propage pas. Si un changement doit toucher plusieurs pages, le
  répéter À L'IDENTIQUE sur chacune, sans introduire de variation.
- Header, navigation et footer sont dupliqués sur chaque page. Toute modif de
  l'un doit être propagée à toutes les pages, à l'identique.
- Les images sont désormais externes dans `/images/`. Ne plus encoder en base64.
- Avant d'éditer une page, vérifier d'où viennent ses styles et ne pas casser la
  cohérence visuelle entre pages.

---

## 2. Architecture du contenu

### Pages produit
- `pack-serenite.html` (offre par abonnement 9,90/14,90 €/mois + éditions papier 60/90 €, anticipateur)

### Pages "situation" (client en crise)
`succession-bloquee`, `conflit-heritiers`, `terrain-familial`, `bien-occupe-heritier`,
`depuis-metropole`, `preparer-succession`, `heritier-refuse`

### Pages "commune" — Guadeloupe (SEO local)
`les-abymes`, `baie-mahault`, `le-gosier`, `pointe-a-pitre`, `petit-bourg`,
`morne-a-l-eau`, `sainte-anne`, `sainte-rose`, `saint-francois`, `gourbeyre`,
`capesterre-belle-eau`, `guadeloupe`, `territoires`

### Pages "commune" — Martinique
`martinique`, `fort-de-france`, `le-lamentin`, `le-robert`, `le-francois`

### Pages "commune" — Guyane
`guyane`, `cayenne`, `kourou`, `saint-laurent-du-maroni`

### Pages "commune" — Autres territoires
`saint-martin` (COM 978, visioconférence, pas de Loi Letchimy)

### Pages "thématique"
`loi-letchimy`, `loi-2026`, `sortie-indivision`, `donation-partage`, `testament`,
`50-pas-geometriques-guadeloupe`, `succession-sans-testament-guadeloupe`,
`heriter-maison-guadeloupe`, `succession-internationale`, `preparation-notaire`,
`guide-succession`, `evaluation`, `mediation`,
`couts-succession-guadeloupe`, `delais-succession-guadeloupe`,
`transmission-patrimoine-guadeloupe`

### Pages "système"
`index`, `nos-services`, `votre-situation`, `ressources`, `conferences`, `equipe`,
`faq`, `temoignages`, `contact`, `mentions-legales`, `confidentialite`

### SEO
`sitemap.xml`, `robots.txt`. NE PAS modifier sans accord explicite.
**Exception accordée** : sitemap.xml peut être modifié pour ajouter de nouvelles pages.

---

## 3. Modèle commercial (à respecter dans tout wording)

Deux portes d'entrée indépendantes, plus un canal terrain.

### Porte 1 — Consultation (parcours d'accompagnement)
- Le client prend rendez-vous GRATUITEMENT avec Luc.
- La consultation gratuite peut déboucher sur un ACCOMPAGNEMENT PAYANT
  (mise en œuvre de la solution de transmission : décider, arbitrer,
  coordonner avec le notaire).
- Cible : client en CRISE (succession bloquée, conflit, indivision).

### Porte 2 — Pack Sérénité (livret par abonnement — grille de juillet 2026)
- Remplace l'ancien pack one-shot à 179 € (abandonné : ne se vendait pas).
  Ne JAMAIS réintroduire le 179 € ni le renouvellement 99 €/an.
- La grille :
  1. ESSENTIEL — 9,90 €/mois : application en ligne + livret PDF (27 pages)
     + support applicatif. SANS conseil sur la transmission.
  2. ACCOMPAGNÉ — 14,90 €/mois : idem + 2 h d'assistance transmission avec Luc.
     2 h AU TOTAL (pas par mois). Objectif business : ces heures servent à
     transformer vers les autres prestations (évaluation, médiation).
  3. Éditions papier : livret personnalisé imprimé 60 € (réservé abonnés) ;
     livret design vierge 90 € (toutes les thématiques, à remplir à la main).
- L'application vit dans le repo jmd971/new_livret_transmiexpert
  (Vercel : new-livret-transmiexpert.vercel.app). Pas encore de paiement en
  ligne : la vente passe par le rendez-vous consultation-livret et le contact.
- Cible : ANTICIPATEUR (pas encore de problème ; veut bien faire pour les siens).
- Un abonné peut ensuite prendre un accompagnement payant avec Luc :
  c'est une suite POSSIBLE, jamais forcée.

### Canal terrain
- Luc intervient chaque mois dans les communes sur le thème de la succession.
  C'est de l'acquisition / notoriété locale, PAS du suivi client mensualisé.

---

## 4. Les deux rendez-vous — URLs exactes, NE JAMAIS CONFONDRE

- CONSULTATION GRATUITE (client en crise, veut parler à Luc) :
  https://my.transmiexpert.fr/widget/bookings/transmiexpert-consultation-initiale
  → CTA des pages "situation" et "commune".

- PACK / MISE EN ROUTE DU LIVRET (incluse dans le Pack 179 €, payant) :
  https://my.transmiexpert.fr/widget/bookings/consultation-livret
  → CTA de TOUS les blocs Pack Sérénité (index, pack-serenite, preparer-succession,
  transmission-patrimoine-guadeloupe).

Règle absolue : un bloc qui parle du Pack / 179 € / livret pointe vers
`consultation-livret`. Un bloc qui propose de parler gratuitement pointe vers
`transmiexpert-consultation-initiale`. Ne jamais inverser.

Autres coordonnées (ne jamais altérer) :
- Tél : 0690 73 45 80 — Email : contact@transmiexpert.fr
- WhatsApp : https://wa.me/590690734580

---

## 5. Positionnement du Pack — hiérarchie du message

Pour tout bloc ou page Pack, dérouler dans cet ordre :
1. Le GESTE qu'on pose pour protéger les siens (fierté, transmission). PAS la peur :
   l'anticipateur n'a pas de crise présente, l'aversion à la perte ne fonctionne pas
   sur lui. Lever sur l'identité ("être celui qui a fait le bon geste") et le legacy.
2. VOUS ÊTES GUIDÉ : l'application guide thème par thème, le client n'a pas
   à savoir par où commencer. Avec la formule Accompagné, Luc répond (2 h incluses,
   au total). C'est ce qui justifie l'abonnement face à un simple document.
3. LE LIVRET à son nom, qui rassemble et sécurise tout (PDF 27 pages ;
   éditions papier possibles : 60 € imprimé abonné, 90 € vierge).
4. PRIX D'ENTRÉE FAIBLE : « dès 9,90 €/mois ». Ne jamais présenter la grille
   comme un catalogue de 4 produits : une porte d'entrée simple, avec options.

- La distinction Essentiel/Accompagné se joue sur l'assistance de Luc : Essentiel
  = support applicatif SEULEMENT (jamais de conseil transmission) ; toujours
  respecter cette frontière dans le wording.
- CTA du Pack = verbe de démarrage accompagné, type "Démarrer mon Pack Sérénité",
  pointant vers `consultation-livret`. Jamais "commander" sec ni "réserver" sec.

---

## 6. Ligne éditoriale

- TransmiExpert n'est NI notaire NI avocat NI expert-comptable. Toujours conserver
  cette mention là où elle figure.
- Ton : premium, chaleureux, institutionnel. Public : familles antillaises 40-70 ans
  + diaspora en Hexagone.
- Pas d'emoji dans le corps de texte. Les icônes UI sont des SVG inline (Lucide).
- Angle dominant du SITE = aversion à la perte (la succession qui traîne coûte cher).
  EXCEPTION : le Pack Sérénité vise l'anticipateur → angle identité / transmission,
  pas la peur (voir section 5).
- Ancrage local réel et digne. Pas de folklore ni de cliché touristique. Créole
  guadeloupéen seulement si pertinent, jamais décoratif, et à faire valider par un
  locuteur natif avant publication.
- Apostrophes et accents : toujours corriger `c est` → `c'est`, `n est` → `n'est`,
  `heritier` → `héritier`, etc. Ne jamais laisser du texte sans accents.

---

## 7. Territoires desservis (confirmé)

| Territoire | Mode d'intervention | Loi Letchimy |
|---|---|---|
| Guadeloupe (971) | Présence physique de Luc | ✅ s'applique |
| Martinique (972) | Visioconférence uniquement | ✅ s'applique |
| Guyane (973) | Visioconférence uniquement | ✅ s'applique |
| Saint-Martin (978) | Visioconférence uniquement | ❌ COM, pas DOM |
| France hexagonale | Visioconférence uniquement | N/A |

**Attention** : Saint-Martin est une collectivité d'outre-mer (COM), pas un département.
La Loi Letchimy ne s'y applique pas — ne jamais l'indiquer sur `saint-martin.html`.

---

## 8. Workflow Claude Code — discipline obligatoire

- UN pas à la fois. Jamais de refonte large en un seul prompt.
- Toujours montrer le DIFF avant d'appliquer une modification.
- COMMIT après chaque étape validée, avec un message clair.
- Fichiers lourds : cibler par grep, ne pas charger les pages entières.
- Ne jamais inventer une information absente. Si une info manque, écrire "À VALIDER"
  et demander, ne pas combler par une supposition.
- `sitemap.xml` : peut être modifié pour ajouter de nouvelles pages (accord donné).
- Ne pas modifier `robots.txt`, `vercel.json` sans accord explicite.

---

## 9. État technique du site (2026-05-29)

### Images
- `/images/` contient les photos externalisées : `luc-silvestre-transmiexpert.jpg`
  + 8 photos conférences. Index.html et equipe.html pointent vers ce dossier.
- Plus aucune image base64 dans les 3 fichiers concernés. Ne pas réintroduire du base64.

### Accessibilité (appliqué sur 54 pages)
- `@media (prefers-reduced-motion: reduce)` : désactive animations/transitions.
- `a:focus-visible, button:focus-visible` : outline vert 3px pour navigation clavier.
- Nav active state : JS injecté avant `</body>`, détecte page courante automatiquement.

### Icônes
- Toutes les icônes UI sont des SVG inline (style Lucide). Ne plus utiliser d'emojis
  comme icônes. `✓`, `✗`, `★` sont du Unicode pur et peuvent rester.

### Communes Guadeloupe
- Les 11 communes ont chacune un sous-titre hero différencié avec une réalité locale
  spécifique. Ne pas copier-coller le même texte entre communes.

### Pages clés à ne pas écraser
- `pack-serenite.html` : repositionnement anticipateur (angle identité/transmission).
- `transmission-patrimoine-guadeloupe.html` : CTA → `consultation-livret` (pas initiale).

---

## 10. À COMPLÉTER / À VALIDER

- [À VALIDER] Tarif exact du renouvellement annuel (affiché 99 €/an — à confirmer).
- [À COMPLÉTER] Logo TransmiExpert pleine couleur sur fond transparent (teal + or).
- [À COMPLÉTER] Témoignages clients réels pour remplacer les témoignages génériques
  (Marie/Jean-Claude/Sylvie dans pack-serenite.html et temoignages.html).
- [À COMPLÉTER] Variations de header/footer si plusieurs versions selon les pages.
