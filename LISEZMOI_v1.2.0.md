# V-Reseller Dashboard 1.2.0 : changements, tests et checklist

## Ce qui change (CHANGELOG)
- **Forfaits activés** : Gratuit / Pro / Expert, avec la licence Gumroad (`LICENSING_ENABLED = true` dans `license.js`).
- `manifest.json` : version **1.2.0**. Ajout de `optional_host_permissions: ["https://api.gumroad.com/*"]`. Cet accès n'est demandé qu'au moment où l'utilisateur active une clé, donc l'extension n'est pas désactivée chez les utilisateurs actuels.
- Popup :
  - **message unique pour les utilisateurs de la 1.1.0** (« la version 1.2 introduit des forfaits… code LANCEMENT30 »), fermable, mémorisé, affiché seulement aux anciens utilisateurs sans licence ;
  - **liens en bas** : Conditions de vente · Mentions légales · Confidentialité (https://miniourse.github.io/v-reseller-privacy/).
- Traductions anglaises ajoutées pour tous les nouveaux textes.
- Fichiers modifiés : `manifest.json`, `license.js`, `popup.html`, `popup.js`, `i18n.js`. **Rien d'autre**, `builder.js` compris, qui est identique à la 1.1.0.

## Rappel des forfaits
- **Gratuit** : Dashboard de l'année en cours.
- **Pro** (5,99 €/mois ou 49 €/an) : toutes les années, coûts d'achat et marges, mois par mois, rentabilité.
- **Expert** (9,99 €/mois ou 89 €/an) : tout le Pro, plus la Compta (journal Excel/FEC, TVA, vitrine).

## Tests passés (38/38)
- Licence, avec un Gumroad simulé :
  - palier Pro, palier Expert, produit « Expert à vie » ;
  - remboursé, abonnement terminé, clé inconnue ;
  - réseau coupé ou Gumroad en panne (la licence est gardée, avec 10 jours de grâce) ;
  - date trafiquée (repasse en Gratuit) ;
  - pas de revérification avant 3 jours.
- Excel : exports Gratuit (2 onglets), Pro et Expert (6 onglets) générés sans erreur. Le rendu Expert est identique à la 1.1.0, puisque `builder.js` n'a pas changé.
- Popup (simulé) :
  - zone forfait, verrous et message 1.2 corrects ;
  - clé fausse et bonne clé Pro gérées ;
  - liens légaux et bouton d'achat corrects ;
  - anglais OK.
- **Non testé, à faire par toi** : un **vrai achat Gumroad** et une vraie clé dans Chrome.

## Checklist avant d'envoyer au Store
1. Gumroad :
   - chaque palier envoie une **clé de licence** ;
   - perte d'accès à la fin de l'abonnement ;
   - remboursement 14 jours ;
   - code **LANCEMENT30** (−30 % à vie, 30 utilisations) ;
   - infos fiscales et paiement avec ton SIRET.
2. Pages légales en ligne **sans case jaune** : adresse, SIRET, médiateur.
3. Test réel :
   - charge le dossier dézippé dans `chrome://extensions` (mode développeur → « Charger l'extension non empaquetée ») ;
   - achète avec un code à 100 % ou utilise le produit « Expert à vie » ;
   - colle la clé, puis vérifie Gratuit → Pro → Expert ;
   - refais le test sur un 2ᵉ PC si possible.
4. Fiche du Store, à modifier toi-même :
   - **Description**, ajouter : « Forfaits : Gratuit (année en cours) · Pro (toutes les années, coûts et marges, mois par mois, rentabilité) · Expert (+ journal comptable Excel/FEC, TVA). Les forfaits payants s'activent avec une clé de licence achetée sur Gumroad. »
   - **Pratiques de confidentialité**, justification de la permission optionnelle : « L'accès à api.gumroad.com est demandé uniquement quand l'utilisateur active une licence payante. Seule la clé de licence est envoyée à Gumroad pour vérifier qu'elle est valide, à l'activation puis environ tous les 3 jours. Aucune donnée de vente ne quitte le navigateur. »
   - **Politique de confidentialité** : https://miniourse.github.io/v-reseller-privacy/#confidentialite
   - **Note de version** : « 1.2.0 : arrivée des forfaits Pro et Expert (licence Gumroad). Le Dashboard de l'année en cours reste gratuit. Code LANCEMENT30 : −30 % à vie pour les 30 premiers clients. »
5. Envoie `v-reseller-dashboard-1.2.0.zip` au Store, toi-même. N'ouvre les ventes qu'après la validation de Google.
