# ☕ Atelier Pratique – Semantic Versioning avec Maven

## Objectif

Appliquer le SemVer à un projet Java/Maven, créer des versions pré-stables et publier des tags/releases sur GitHub. Le dossier `maven-project` contient un mini-projet Maven prêt à l'emploi.

## Pré-requis

- JDK 11+ installé et `mvn` en PATH
- Git configuré et un remote GitHub prêt

## 1️⃣ Créer / ouvrir le projet Maven

La structure fournie :

```
maven-project/
├─ pom.xml   # version initiale 1.0.0
├─ src/
│  └─ main/java/com/sdley/App.java
└─ README.md
```

Extrait `pom.xml` :

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.sdley</groupId>
  <artifactId>semver-demo-maven</artifactId>
  <version>1.0.0</version>
</project>
```

## 2️⃣ Initialiser Git et premier commit

```bash
git init
git add .
git commit -m "chore: initial project v1.0.0"
git branch -M main
git remote add origin <git_remote_url>
git push -u origin main
```

## 3️⃣ Utiliser Maven Versions Plugin pour bump

Ajoute le plugin (ex. déjà inclus dans le `pom.xml` fourni).

### Bump mineur

```bash
mvn versions:set -DnewVersion=1.1.0
git add pom.xml
git commit -m "feat: bump to 1.1.0"
git tag v1.1.0
git push origin main --tags
```

### Bump patch

```bash
mvn versions:set -DnewVersion=1.1.1
git add pom.xml
git commit -m "fix: bump to 1.1.1"
git tag v1.1.1
git push origin main --tags
```

## 4️⃣ Pré-versions (alpha/beta/rc)

Maven n'impose pas un format mais accepte n'importe quelle chaîne valide dans `<version>` :

```bash
mvn versions:set -DnewVersion=1.2.0-alpha-1
git commit -am "chore(release): 1.2.0-alpha-1"
git tag v1.2.0-alpha-1
git push origin main --tags
```

> Exemple d'utilisation d'un suffixe numérique `-alpha-1`, `-beta-2`, `-rc-1`.

## 5️⃣ Métadonnées de build

Ajoute dans le `pom.xml` :

```xml
<version>1.2.0+build.20251025</version>
```

Note : certains outils Maven peuvent refuser certaines métadonnées ; utilisez-les surtout pour documentation ou CI.

## 6️⃣ Release GitHub

Pousser les tags et créer une release depuis GitHub (comme pour npm). Inclure changelog et notes.

## 7️⃣ Commandes utiles pour la démo live

```bash
mvn -v
mvn clean package
mvn versions:display-dependency-updates
```

## Résultat attendu

- `pom.xml` mis à jour selon SemVer
- Tags Git visibles sur GitHub
- Release GitHub documentée

## Script de démonstration (optionnel)

Un script `demo-maven.sh` est inclus pour automatiser les étapes de version bump et création de tag (à exécuter localement).
