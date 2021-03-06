# spip_svn_loader
Installer et mettre à jour SPIP avec SVN

## SPIP et SubVersioN

[SPIP](http://www.spip.net) est un CMS écrit en PHP et développé sous SVN. Pour des raisons historiques, ses branches et tags sont organisées de telles manières qu'il est aujourd'hui facile de se perdre. :)

Ce script permet de guider une personne souhaitant installer ou mettre à jour une instance SPIP avec Subversion.

## Pré-requis

- *bash*. Ce script est écrit en bash sur un Mac OS X (GNU bash, version 3.2.57) mais se veut compatible avec les plates-formes linux (testé sur Ubuntu 14 et mingw64). Pour s'en servir, il faut savoir ouvrir un terminal... :)
- *subversion*. Ce script caclule et exécute des lignes de commandes du type `svn info`, `svn checkout`, `svn switch`, etc. Votre machine doit disposer d'un client subversion (`svn`) installé et configuré dans le `$PATH`.
- *curl*. Pour installer et tenir à jour la liste des branches de référence décrite plus bas, ce script utilise la commande [cURL](https://curl.haxx.se/) qui doit, elle aussi, être configurée dans le `$PATH`.
- *php*. Ce script vérifie la version de [PHP](http://www.php.net) installée et configurée comme les outils ci-dessus.

S'il manque un des outils ci-dessus, le script vous le dira.

## Branches de développement, de maintenance ou release

- Le trunk de SPIP n'est pas `trunk` mais `spip`. Le script y fera référence en parlant de `dev`.
- Les branches de maintenance historiques de SPIP sont nombreuses. Elles se trouvent dans le répertoire `branches` du dépôt officiel de SPIP. Le script y fera référence en parlant de `maintenance`.
- Les versions alpha, beta, RC ou stable de SPIP se trouvent dans le répertoire `tags` du dépôt officiel de SPIP. Le script y fera référence en parlant de `release`.

Lors du choix de version que proposera le script, avant de décider d'une version précise, le script proposera de pré-sélectionner une de ces branches.

## Installation

- [Téléchargez](https://raw.githubusercontent.com/JamesRezo/spip_svn_loader/1.0.0-beta2/spip_svn_loader) le script dans le répertoire `/usr/local/bin` ou tout autre répertoire configuré dans votre `$PATH`.
- Le rendre exécutable ```chmod +x /usr/local/bin/spip_svn_loader``.

Alternativement, ```git clone https://github.com/JamesRezo/spip_svn_loader.git``` et un lien symbolique ```ln -s `pwd`/spip_svn_loader/spip_svn_loader /usr/local/bin/spip_svn_loader``` marche aussi bien...

Avec [Homebrew](http://brew.sh/) pour les utilisateurs de Mac OS X:
```bash
brew tap JamesRezo/spip
brew install spip_svn_loader
```

## Usage

Dans le répertoire cible, taper `spip_svn_loader`.

### Le répertoire cible est déjà associé à une branche SVN de SPIP.

Le script tente de détecter la branche associée.

* Si la branche est maintenue, il proposera de faire une mise à jour (`svn up`)
* Si la branche n'est plus maintenue (ou a été supprimée), il proposera de basculer vers une branche existante (`svn switch`)

### Le répertoire cible n'est pas associé à une branche SVN.

Qu'il soit vide ou pas, le script tentera d'y installer (`svn checkout`) la version choisie. S'il s'agit d'une `release`, il proposera de détacher le répertoire du dépôt SVN (`svn export`) mais vous pourrez refuser et attacher le répertoire au dépôt SVN (peut-être pour basculer vers une autre release dans le futur).

### Le répertoire cible est déjà associé à une branche SVN d'autre chose.

Si le répertoire est déjà associé à un dépôt SVN (_working copy_), le script tentera d'installer la version choisie dans un sous-répertoire `spip` qui sera créé pour l'occasion. Comme ci-dessus, s'il s'agit d'une `release`, la même proposition de détachement sera faite.

## Liste des branches de référence

Le script exploite, par défaut, une liste de branches que je considère comme _utiles_. Elle se trouve [ici](http://james.at.rezo.net/svn_spip/svn_spip.txt). Cette liste sera téléchargée (`${HOME}/.spip/svn_loader_references.txt`) et mise à jour automatiquement quand la liste évoluera.

## Usage avancé

Ajouter le paramètre `tout` pour accéder à toutes les branches et tous les tags SPIP disponibles sur le dépôt officiel: ```spip_svn_loader tout```
