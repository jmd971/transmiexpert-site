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
- `pack-serenite.html` (offre 179 €, anticipateur)

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

### Porte 2 — Pack Sérénité (produit, 179 €)
- 179 € = un DÉMARRAGE ACCOMPAGNÉ de la mise en ordre patrimoniale. Il comprend :
  1. un rendez-vous de MISE EN ROUTE avec Luc (le client n'est jamais seul face
     au document — c'est le cœur de la valeur, à dire tôt et clairement) ;
  2. un LIVRET patrimonial personnel, à son nom, qui rassemble et sécurise tout
     au même endroit ;
  3. la PREMIÈRE ANNÉE d'abonnement INCLUSE : possibilité de poser une question
     à tout moment.
- L'abonnement se renouvelle ensuite chaque année (service à la demande, pas de
  mise à jour push). Renouvellement affiché 99 €/an dans pack-serenite.html —
  [À VALIDER] si ce tarif est définitif.
- Cible : ANTICIPATEUR (pas encore de problème ; veut bien faire pour les siens).
- Un acheteur du Pack peut ensuite prendre un accompagnement payant avec Luc :
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
2. ON LE FAIT AVEC VOUS : le rendez-vous de mise en route inclus. Le client n'a pas
   à savoir par où commencer. C'est ce qui justifie 179 € face à un simple document.
3. LE LIVRET à son nom, qui rassemble et sécurise tout.
4. LA TRANQUILLITÉ INCLUSE UN AN : une question, un doute, un courrier du notaire —
   quelqu'un répond.

- Ne PAS vendre "un livret + un abonnement" comme deux choses : l'abonnement est
  une QUALITÉ du produit (tranquillité garantie un an), pas une ligne de prix.
- Mention du renouvellement annuel : transparente mais discrète, jamais l'argument
  principal.
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
