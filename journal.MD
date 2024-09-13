# Rapport de Lecture
## Encart
Rust est un langage performant, il peut s'intégrer à d'autres langage , il est aussi économe en mémoire et fonctionné sur des système embarqués.<br>
Le système de typages et le modèle d'ownership de Rust est fiable grâce à la sécurité mémoire et des threads.<br>
Rust offre une documentation claire, un compilateur avec des messages d'erreur utiles, et des outils comme un gestionnaire de paquet intégré

## Avant-Propos
Rust permet aux développeurs d'écrire du code sûrs tout en veillant à corriger les erreurs critique , performant dans divers domaine notamment dans le bas niveau mais aussi il peut contribuer à des applications web, tout en evitant les problèmes liés à la gestion de mémoire.


## Introduction
Rust s'adresse à tout le monde, étudiant, entreprises, développeurs de logiciel libre. Il se révèle être un un outil productif pour la collaboration.
Le code de bas-niveau est sujet à une multitude de bogues et qui ne peuvent être detecté qu'au moyen de test et relecture des developpeurs chevronnées.<br>
Le compilateur Rust empêche la compilation de code contenant des bugs subtils et complexes, y compris des bogues de concurrence, ce qui améliore la productivité d'une équipe de développeurs en réduisant les erreurs et en sécurisant le code dès la phase de développement.
Il est une solution pour les personnes qui recherchent de la rapidité et de la stabilité 


### 1.1 - Installation de Rust 
#### 1. Installez Rust sur Linux ou macOS :
```bash
$ curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
```
Vous devez installer si vous êtes sur macOS le compilateur c
```bash
$ xcode-select --install
```
Si l'installation est réussi vous avez ce message
```bash
Rust is installed now. Great!
```
#### 2. Dépannage
Il nous faut vérifier si Rust est correctement installé
```bash
$ rustc --version
```
on devrait avoir un message du type 
```bash
rustc x.y.z (abcabcabc yyyy-mm-dd)
```
#### 3. Mettre à jour et desinstaller Rust
Pour mettre à jour Rust
```bash
$ rustup update
```
Pour desinstaller Rust
```bash
$ rustup self uninstall
```
### 1.2 - Écrire et exécuter un programme Rust
Un script sur Rust s'écrit de cette manière là
```bash
fn main() {
    println!("Hello, world!");
}
```
Pour éxécuter ce script il faut effectué ces commandes:
```bash
$ rustc main.rs
$ ./main
```
Le programme devrait nous retourner :
```bash
Hello, world!
```
La fonction ```main``` est le point d'entrée de tous les programmes en Rust. Elle est définie sans paramètres et sans valeur de retour, avec son corps délimité par des accolades {}. 
À l'intérieur de la fonction main, nous avons le code suivant 
```println!("Hello, world!");```.

## Mes questions
Comment Rust s'intègre t-il dans d'autre langage ?<br>
Comment est gérer la mémoire en Rust ?<br>
Comment se differencie t-il des autres langages de programmation ?<br>
Expliquez en quoi Rust permet au développeur de corriger efficacement les erreurs.<br>
C'est quoi "un bogues de concurrence" ?<br>


###### Jonny MATHANARUBAN