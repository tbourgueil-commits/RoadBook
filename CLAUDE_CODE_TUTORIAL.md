# Tutoriel : Comment fonctionne Claude Code

Claude Code est un assistant de développement en ligne de commande (CLI) conçu par Anthropic. Il vous aide à écrire, comprendre, modifier et déboguer du code directement dans votre terminal.

---

## 1. Qu'est-ce que Claude Code ?

Claude Code est une interface qui permet à Claude (le modèle d'IA d'Anthropic) d'interagir directement avec votre projet. Contrairement à un chatbot classique, Claude Code peut :

- **Lire et modifier des fichiers** de votre projet
- **Exécuter des commandes** dans le terminal
- **Rechercher du code** dans toute la base de code
- **Faire des commits Git** et pousser des branches
- **Analyser des erreurs** et proposer des corrections

---

## 2. Installation

```bash
# Installer Claude Code via npm
npm install -g @anthropic-ai/claude-code

# Vérifier l'installation
claude --version
```

---

## 3. Lancer Claude Code

```bash
# Dans le dossier de votre projet
cd /votre/projet

# Démarrer une session interactive
claude
```

Une fois lancé, vous pouvez taper des instructions en langage naturel directement dans le terminal.

---

## 4. Exemples d'utilisation

### Comprendre une base de code existante

```
> Explique-moi comment fonctionne la gestion de la base de données IndexedDB dans ce projet
```

Claude va lire les fichiers pertinents et vous expliquer le code.

### Ajouter une fonctionnalité

```
> Ajoute un bouton pour exporter les données du voyage au format CSV
```

Claude va analyser le code existant, écrire la nouvelle fonctionnalité, et modifier les fichiers nécessaires.

### Corriger un bug

```
> L'enregistrement audio ne fonctionne pas sur iOS, trouve et corrige le problème
```

Claude va rechercher les causes possibles et proposer une correction.

### Refactoriser du code

```
> La fonction saveStep() est trop longue, divise-la en fonctions plus petites
```

---

## 5. Les outils que Claude Code utilise

Claude Code dispose d'outils internes pour interagir avec votre projet :

| Outil | Description |
|-------|-------------|
| `Read` | Lire le contenu d'un fichier |
| `Write` | Créer ou réécrire un fichier |
| `Edit` | Modifier une partie spécifique d'un fichier |
| `Glob` | Rechercher des fichiers par pattern (ex: `**/*.js`) |
| `Grep` | Rechercher du texte dans les fichiers |
| `Bash` | Exécuter des commandes shell |

Claude choisit automatiquement quel outil utiliser selon votre demande.

---

## 6. Gestion des permissions

Avant d'exécuter certaines actions potentiellement risquées, Claude Code vous demande confirmation. Par exemple :

- Écriture dans des fichiers
- Exécution de commandes système
- Opérations Git (commit, push)

Vous pouvez configurer le niveau de permission (`auto`, `manual`, ou par commande spécifique).

---

## 7. Workflow Git avec Claude Code

Claude Code peut gérer tout le cycle Git pour vous :

```
> Crée une nouvelle branche, ajoute la fonctionnalité de filtre par date, puis fais un commit et push
```

Ce que Claude fera automatiquement :
1. `git checkout -b feature/filtre-date`
2. Modifier les fichiers nécessaires
3. `git add <fichiers modifiés>`
4. `git commit -m "Ajoute un filtre par date pour les voyages"`
5. `git push -u origin feature/filtre-date`

---

## 8. Fichier CLAUDE.md — Instructions permanentes

Vous pouvez créer un fichier `CLAUDE.md` à la racine de votre projet pour donner des instructions persistantes à Claude :

```markdown
# Instructions pour Claude

## Contexte du projet
RoadBook est une PWA de carnet de voyage en français.

## Conventions de code
- Commentaires en français
- Indentation : 2 espaces
- Pas de frameworks JavaScript externes

## Commandes utiles
- Ouvrir dans le navigateur : `python3 -m http.server 8080`
```

Claude lira ce fichier automatiquement à chaque session.

---

## 9. Modes de fonctionnement

### Mode interactif (par défaut)
```bash
claude
```
Session conversationnelle continue dans votre terminal.

### Mode commande unique
```bash
claude -p "Résume ce que fait le fichier index.html"
```
Exécute une seule instruction et retourne le résultat.

### Mode sans confirmation automatique
```bash
claude --dangerously-skip-permissions
```
⚠️ À utiliser avec précaution — Claude exécutera toutes les actions sans demander confirmation.

---

## 10. Bonnes pratiques

1. **Soyez précis dans vos demandes** : "Ajoute un champ 'météo' au formulaire d'étape" est mieux que "améliore le formulaire".

2. **Travaillez par petites étapes** : Demandez une fonctionnalité à la fois pour garder le contrôle.

3. **Vérifiez les modifications** : Après chaque changement, lisez le code modifié pour vous assurer qu'il correspond à vos attentes.

4. **Utilisez Git** : Faites des commits réguliers. En cas de problème, vous pouvez toujours revenir en arrière avec `git revert`.

5. **Rédigez un CLAUDE.md** : Donnez le contexte de votre projet dès le départ pour de meilleurs résultats.

---

## 11. Exemple complet : ajouter une fonctionnalité à RoadBook

Voici un exemple concret d'interaction avec Claude Code sur ce projet :

```
Utilisateur : Ajoute une fonctionnalité pour noter chaque étape de 1 à 5 étoiles

Claude : Je vais d'abord lire le code existant pour comprendre la structure des étapes...
[lit index.html]

Je vais ajouter :
1. Un sélecteur d'étoiles dans le formulaire d'étape (openStepModal)
2. Un champ `rating` dans la structure de données de l'étape
3. L'affichage des étoiles dans renderSteps()

Voici les modifications...
[modifie index.html]

Les changements sont faits. Voulez-vous que je fasse un commit ?

Utilisateur : Oui, fais le commit et push

Claude :
[git add index.html]
[git commit -m "Ajoute un système de notation par étoiles pour les étapes"]
[git push -u origin feature/notation-etoiles]

Commit effectué et poussé sur la branche feature/notation-etoiles.
```

---

## Ressources

- Documentation officielle : [docs.anthropic.com/claude-code](https://docs.anthropic.com/en/docs/claude-code)
- Signaler un problème : [github.com/anthropics/claude-code/issues](https://github.com/anthropics/claude-code/issues)
- Aide dans le terminal : tapez `/help` dans une session Claude Code
