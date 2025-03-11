# Manuel d'installation du Dashboard Rust/Egui

Ce manuel décrit les étapes nécessaires pour installer et exécuter le projet Dashboard Rust/Egui.

## Prérequis

Avant de commencer, assurez-vous d'avoir les éléments suivants installés sur votre système :

- [Rust](https://www.rust-lang.org/tools/install) (version stable recommandée)
- [Cargo](https://doc.rust-lang.org/cargo/getting-started/installation.html) (inclus avec Rust)
- [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

## Étapes d'installation

### 1. Cloner le dépôt

Clonez le dépôt GitHub du projet sur votre machine locale :

```bash
git clone https://github.com/info5-groupe-9-dashboard-rust/app.git
cd app
```

### 2. Installer les dépendances

Utilisez Cargo pour installer les dépendances du projet :

```bash
cargo build
```

### 3. Compiler le projet

Compilez le projet en utilisant Cargo :

```bash
cargo build --release
```

> L'option `--release` est utilisée pour compiler le projet en mode de production.
### Compilation croisée pour Windows

Si vous souhaitez compiler l'application pour Windows depuis un système Linux :

1. Ajoutez la cible Windows :
    ```bash
    rustup target add x86_64-pc-windows-gnu
    ```

2. Installez le linker MinGW nécessaire pour la compilation croisée :
    ```bash
    sudo apt install gcc-mingw-w64-x86-64 g++-mingw-w64-x86-64 mingw-w64
    ```

3. Compilez votre projet Rust pour Windows :
    ```bash
    cargo build --release --target x86_64-pc-windows-gnu
    ```

> L'exécutable Windows sera disponible dans le dossier `target/x86_64-pc-windows-gnu/release/`

### 4. Exécuter le projet

Une fois la compilation terminée, vous pouvez exécuter le projet :

```bash
cargo run
```

## Exécution dans un navigateur (WebAssembly)

### Exécution dans un navigateur (WebAssembly)

#### Préparation pour le web

Pour exécuter l'application comme une application web à l'aide de WebAssembly :

1. Ajoutez la cible WASM :
    ```bash
    rustup target add wasm32-unknown-unknown
    ```

2. Installez Trunk :
    ```bash
    cargo install --locked trunk
    ```

3. Servez localement :
    ```bash
    trunk serve
    ```
    Accédez à l'application via `http://127.0.0.1:8080/index.html#dev`

> Ajoutez `#dev` à l'URL pour éviter la mise en cache PWA pendant le développement

#### Déploiement web

1. Construisez pour la production :
    ```bash
    trunk build --release
    ```

2. Déployez le répertoire `dist` généré sur votre plateforme d'hébergement préférée

> L'application prend en charge la fonctionnalité hors ligne grâce à la mise en cache du service worker !

## Executer les releases

### Téléchargement des releases

Les releases du projet sont disponibles sur la page GitHub du projet. Pour télécharger la dernière version stable :

1. Accédez à la page des releases : https://github.com/info5-groupe-9-dashboard-rust/app/releases
2. Téléchargez la version correspondant à votre système d'exploitation :
    - `.exe` pour Windows
    - Fichier binaire (sans extension) pour Linux
    - `.dmg` ou `.app` pour macOS

### Exécution des fichiers binaires

#### Windows
- Double-cliquez sur le fichier `.exe` téléchargé
- Ou exécutez-le depuis l'invite de commande :
  ```cmd
  chemin\vers\dashboard.exe
  ```

#### Linux
1. Rendez le fichier binaire exécutable :
    ```bash
    chmod +x chemin/vers/dashboard
    ```
2. Exécutez l'application :
    ```bash
    ./chemin/vers/dashboard
    ```

#### macOS
- Double-cliquez sur le fichier `.dmg` pour le monter
- Glissez l'application dans votre dossier Applications
- Ou exécutez directement l'application `.app`

### Vérification d'intégrité

Pour vérifier l'intégrité du fichier téléchargé, utilisez la somme de contrôle SHA-256 fournie avec chaque release :

```bash
sha256sum chemin/vers/fichier_téléchargé
```

Comparez le résultat avec la somme de contrôle disponible sur la page de release.

## Problèmes courants

### Erreurs de compilation

Si vous rencontrez des erreurs de compilation, assurez-vous que toutes les dépendances sont correctement installées et que vous utilisez la version stable de Rust.

### Problèmes de dépendances

Si des problèmes de dépendances surviennent, essayez de mettre à jour Cargo :

```bash
cargo update
```

## Conclusion

Vous avez maintenant installé et exécuté le projet Dashboard Rust/Egui. Pour plus de détails sur l'utilisation et la contribution, veuillez consulter la documentation du projet.
