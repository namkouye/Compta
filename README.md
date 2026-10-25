# Northstar Books — prototype PWA local-first

Prototype de départ pour une application de comptabilité de corporation canadienne (BC / Ontario).

## Lancer l'application

Comme l'application utilise IndexedDB et un service worker, il faut la servir depuis `localhost` ou HTTPS (ne pas ouvrir simplement `index.html` avec `file://`).

### Option Python
Dans ce dossier, lancer :

```bash
python3 -m http.server 8080
```

Puis ouvrir `http://localhost:8080` dans Chrome, Edge ou Safari récent.

### Installation comme PWA
Sur un navigateur compatible, utiliser « Installer l'application » ou « Ajouter à l'écran d'accueil » depuis le menu du navigateur. Le service worker met en cache les fichiers de l'interface pour un accès hors ligne après le premier chargement.

## Fonctionnalités présentes dans ce prototype

- Dashboard simple.
- Plan comptable de départ.
- Saisie manuelle des transactions.
- Import CSV de transactions bancaires (importation générique; chaque fichier doit être contrôlé).
- Archivage local de reçus/PDF/images et association à une transaction.
- Marquage manuel des transactions comme rapprochées.
- Rapports de gestion simplifiés.
- Export CSV et sauvegarde/restauration JSON.

## Limites importantes

Ce n'est PAS encore un système comptable complet et ne doit pas être utilisé comme source officielle pour produire des déclarations fiscales sans validation. La saisie actuelle ne crée pas encore un véritable journal en partie double équilibré : elle enregistre les transactions et calcule des totaux de gestion.

Avant toute utilisation réelle, il faut notamment construire et tester :
1. Écritures de journal en partie double avec débit = crédit.
2. Soldes d'ouverture, rapprochement bancaire avec soldes de relevé, détection des doublons et gestion des virements entre comptes.
3. Comptes clients/fournisseurs, facturation et paiements partiels.
4. Gestion détaillée de GST/HST/PST, crédits de taxe sur intrants, remises et règles de lieu de fourniture.
5. Immobilisations, amortissements, paie si nécessaire et clôture d'exercice.
6. Audit log append-only, verrouillage des périodes et corrections par contre-écriture.
7. Sauvegarde chiffrée, contrôle d'intégrité et tests de restauration.
8. Tests comptables et validation par un CPA canadien.

## Stockage et confidentialité

Les données sont stockées dans IndexedDB sur le navigateur et le profil local utilisé. Elles ne sont pas automatiquement synchronisées entre appareils. Les reçus et pièces jointes sont incorporés dans la sauvegarde JSON; les sauvegardes peuvent donc contenir des informations financières sensibles. Conserve-les dans un emplacement sécurisé et ne les partage pas sans précaution.

## Architecture actuelle

- Interface : HTML/CSS/JavaScript sans dépendance externe.
- Stockage : IndexedDB.
- Hors ligne : service worker + cache des ressources.
- Portabilité : export CSV et sauvegarde JSON.
- Devise d'affichage : CAD.
