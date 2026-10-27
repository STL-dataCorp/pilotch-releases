# PilotCH — Application Windows

Ce dépôt contient uniquement les **installateurs Windows** de PilotCH (ERP BTP).
Le code de l'application reste dans un dépôt privé.

**Télécharger PilotCH :** onglet [Releases](../../releases), dernière version, fichier `PilotCH-Setup-x.y.z.exe`.

---

## Installer PilotCH sur un PC

1. Télécharger `PilotCH-Setup-x.y.z.exe` dans [Releases](../../releases) (rubrique **Assets**).
2. Ouvrir le fichier. Si Windows affiche « Windows a protégé votre ordinateur » :
   cliquer **Informations complémentaires**, puis **Exécuter quand même**
   (normal tant que l'application n'a pas de certificat de signature).
3. Suivre l'installation (**Suivant**, puis **Installer**). Un raccourci PilotCH est créé sur le bureau.
4. Se connecter avec son compte PilotCH habituel.

Les mises à jour arrivent toutes seules : PilotCH les télécharge et propose de redémarrer.

---

## Publier une nouvelle version (réservé à l'éditeur)

Tout se fait sur GitHub, depuis le dépôt privé du code.

1. Onglet **Actions** › **Application Windows** › bouton **Run workflow**.
2. Laisser **Branch: main**, taper la nouvelle version, toujours plus grande que la précédente
   (`1.0.1`, `1.1.0`, `2.0.0`…), puis **Run workflow**.
3. Attendre environ 10 minutes la coche verte.
4. La version apparaît ici, dans [Releases](../../releases). Les PC déjà installés la reçoivent seuls.

Utiliser **Run workflow** (nouvelle exécution), pas « Re-run », pour prendre les dernières modifications du code.

---

## Mise en place (déjà faite, à refaire seulement en cas de problème)

1. **Ce dépôt public** `pilotch-releases`, propriétaire `STL-dataCorp`, avec au moins un fichier
   (ce README). Un dépôt vide refuse la création des versions.
2. **Un jeton GitHub** (Settings › Developer settings › Personal access tokens › Fine-grained tokens) :
   - Token name : `pilotch-releases`
   - Resource owner : `STL-dataCorp`
   - Expiration : 1 an au plus (une date est obligatoire)
   - Repository access : **Only select repositories** › `pilotch-releases`
   - Permissions : **Contents : Read and write** (Metadata : Read-only s'ajoute seul)
   - Le jeton ne s'affiche qu'une fois. Ne jamais l'écrire ici ni le donner à quelqu'un.
3. **Dans le dépôt privé du code** › Settings › Secrets and variables › Actions :
   - Secret `RELEASES_TOKEN` = le jeton seul (commence par `github_pat_`), sans guillemets ni espace.
   - Variable `API_URL` = `https://pilotch-api.onrender.com`
   - Variable `RELEASES_REPO` = `pilotch-releases`
   - Noms tapés au clavier : lettres, chiffres et `_` uniquement, sans espace.

### Le jeton expire

Créer un nouveau jeton (étape 2), puis remplacer la valeur du secret `RELEASES_TOKEN` (étape 3).

### Erreurs déjà rencontrées

| Message dans Actions | Cause | Solution |
| --- | --- | --- |
| `Personal Access Token … contains invalid characters` | Espace ou texte en trop collé avec le jeton | Recoller le jeton seul dans `RELEASES_TOKEN` |
| `Published releases must have a valid tag` | Ce dépôt était vide | Ajouter un fichier (ce README) |
| `Variable API_URL manquante` | Variable absente | Ajouter `API_URL` (étape 3) |
| `Version invalide` | Version mal tapée | Taper trois nombres séparés par des points : `1.0.1` |
| Le jeton est refusé à la création | Jeton sans date d'expiration | Choisir une date (1 an au plus) |
