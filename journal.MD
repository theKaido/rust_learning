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

## I - Prise en main
### 1.1 - Installation de Rust 
Il est assez facile à installer rust et à gerer les différent version de Rust:
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
Un script sur Rust s'écrit comme en C de là manière suivante 
```rust
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
La fonction `main` est le point d'entrée de tous les programmes en Rust. Elle est définie sans paramètres et sans valeur de retour, avec son corps délimité par des accolades {}. 
À l'intérieur de la fonction main, nous avons le code suivant 
`println!("Hello, world!");`.<br>
Il écrit le texte à l'écran. Il y a quatre détails importants à noter ici:
 - l'identation 4 espaces.
 - println! est une macro propre à Rust.
 - "Hello, world!" est une chaîne que nous envoyons en argument à println!.
 - le point-virgule (;) indique que cette expression est terminée. 

La compilation et l'éxécution sont des étapes séparées en Rust comme en C.

### 1.3 - Cargo
Cargo est le système de compilation et de gestion de paquets de Rust.<br>
Il va nous permettre de gerer le projet en cours.<br>


Pour créer un projet en cargo voici les étapes à suivre
```rust
$ cargo new hello_cargo
$ cd hello_cargo
```
Cette commande permet de créer un nouveau projet.<br>
Pour compiler ce projet : 
```rust
$ cargo build
   Compiling hello_cargo v0.1.0 (file:///projects/hello_cargo)
    Finished dev [unoptimized + debuginfo] target(s) in 2.85 secs
```
Une fois le projet compiler il ne reste plus qu'a l'éxécuter:
```rust
$ cargo run
    Finished dev [unoptimized + debuginfo] target(s) in 0.0 secs
     Running `target/debug/hello_cargo`
Hello, world!
```
Cargo fournit aussi une commande appelée `cargo check`. Elle vérifie rapidement votre code pour s'assurer qu'il est compilable, mais ne produit pas d'exécutable

Cargo simplifie le processus de création, de compilation, et d'exécution des programmes, tout en gérant automatiquement les dépendances externes, il aide à structurer les projets en organisant les fichiers source et les configurations, tout en offrant des commandes pratiques comme cargo build (compilation), cargo run (exécution) et cargo check (vérification rapide sans exécutable).

## II - Programmer le jeu du plus ou du moins
Il nous faut d'abord créer le projet (voir le chapitre 1.3 Cargo)<br>
La première partie du programme consiste à demander au joueur de saisir du texte, à traiter cette saisie, et à vérifier que la saisie correspond au format attendu en voici un exemple:
```rust
use std::io;

fn main() {
    println!("Devinez le nombre !");

    println!("Veuillez entrer un nombre.");

    let mut supposition = String::new();

    io::stdin()
        .read_line(&mut supposition)
        .expect("Échec de la lecture de l'entrée utilisateur");

    println!("Votre nombre : {}", supposition);
}
```
Pour obtenir la saisie utilisateur et ensuite l'afficher, nous avons besoin d'importer la bibliothèque d'entrée/sortie `io` <br>
Comme mentionnée dans le chapitre précedent `main` est le point d'entrée du programme <br>
Le mot clé `fn` déclare une nouvelle fonction, les parenthèses `()` indiquent que cette fonction n'accepte aucun paramètre, et l'accolade ouvrante `{` marque le début du corps de la fonction.<br>
Ensuite, on crée une variable pour stocker la saisie de l'utilisateur, comme ceci :
```rust
let mut supposition = String::new();
```
Ici nous pouvons noté que le mot clé `mut` est important car en Rust les variables sont immuable losqu'elles sont déclarées , il nous faut donc les rendre mutable en ajoutant le mot clé `mut`lors d'une déclaration de variables permet de modifier la valeur contenue dans celle-ci.<br>

la fonction `stdin` du module `io` permet de traiter la valeur saisie par l'utilisateur <br>
la méthode `read_line` sur l'entrée standard afin de récuperer la valeur saisie par utilisateur et de l'affecté à la variable `supposition`, on utilise la référence de la variable (`&`) , la référence permet de laisser plusieurs morceaux de votre code accéder à une même donnée sans avoir besoin de copier ces données dans la mémoire plusieurs fois.
On gére les erreurs à l'aide de la ligne 
```rust
.expect("Échec de la lecture de l'entrée utilisateur");
```


Pour générer un nombre aléatoire dans le jeu du plus ou du moins, nous utilisons la crate externe `rand`. D'abord, nous ajoutons cette dépendance dans le fichier `Cargo.toml` :

```toml
[dependencies]
rand = "0.8.3"
```
Ensuite, dans le code, on importe le trait `rand::Rng`, qui permet d'accéder aux méthodes de génération de nombres aléatoires :
```rust
use rand::Rng;
```
Le générateur de nombres est créé avec `rand::thread_rng()`, qui fournit un générateur spécifique au thread actuel. La méthode`gen_range(1..101)` est utilisée pour générer un nombre entre 1 et 100:
```rust
let nombre_secret = rand::thread_rng().gen_range(1..101);
```
Le résultat est ensuite stocké dans une variable, et ce nombre sera celui que l'utilisateur devra deviner.<br>


Une fois que l'utilisateur a saisi un nombre, nous pouvons le comparer au nombre secret. Pour cela, nous utilisons la méthode `cmp` sur la supposition de l'utilisateur. Cette méthode compare deux valeurs et retourne une énumération `Ordering` avec trois variantes : `Less`, `Greater`, ou `Equal`.

Nous commençons par importer `std::cmp::Ordering`

```rust
use std::cmp::Ordering;
```
Ensuite, nous utilisons une expression match pour comparer la supposition au nombre secret :
```rust
match supposition.cmp(&nombre_secret) {
    Ordering::Less => println!("C'est plus !"),
    Ordering::Greater => println!("C'est moins !"),
    Ordering::Equal => {
        println!("Vous avez gagné !");
        break;
    }
}
```
Ajouter la ligne `break` après "Vous avez gagné !" fait sortir le programme quand le joueur a correctement deviné le nombre secret. Et quitter la boucle veut aussi dire terminer le programme, car ici la boucle est la dernière partie de main.

## III - Les concepts courants de programmation
Nous allons voir ici les concepts courant présent dans presque tout les langages de programmation , et comment il fonctionne en Rust.
Les variables , les types les fonctions , les commentaires, les structures de contrôle seront abordés dans ce chapitre.
Rust possède un ensemble de mots-clé reservé à celui ci , nous ne pouvons pas les utilisé comme nom de variables ou de fonctions, ces mots-clés ont des signification spéciale, et nous servir à rediger différent programme en Rust. 
### A - Les variables et la mutabilité 
En Rust, les variables sont immuables par défaut, ce qui garantit la sécurité et évite des bugs difficiles à traquer. Une fois qu'une variable est assignée, elle ne peut pas être modifiée, ce qui permet de garder un code plus sûr. Cependant, on peut rendre une variable mutable avec le mot-clé **mut** si on doit la modifier.
Si vous avez besoin de modifier la valeur d'une variable, vous devez la déclarer avec mut, ce qui permet d'indiquer explicitement que la variable peut changer au cours du programme. Cela rend votre intention claire pour d'autres développeurs qui liront votre code.

L'immuabilité est encouragée car elle rend le code plus fiable et évite les erreurs difficiles à détecter, comme les bogues de concurrence. Par exemple, si une partie du code repose sur une variable immuable, elle peut avoir des garanties que cette valeur ne changera pas, ce qui simplifie la logique du programme. La mutabilité peut être utile dans certains cas, notamment lorsqu'il est plus performant de modifier directement une structure de données existante plutôt que d'en créer une nouvelle. Cependant, il est souvent conseillé de choisir la clarté du code (en créant de nouvelles instances) plutôt que de rechercher la performance dans des cas où les données sont petites.

Contrairement aux variables immuables, les constantes sont toujours immuables et doivent être déclarées avec **const** et un type explicite. Elles sont souvent utilisées pour des valeurs qui ne changent pas et qui sont partagées entre plusieurs parties d'un programme. Elles doivent être initialisées avec des expressions calculables à la compilation.
Rust permet également de redéclarer une variable avec le même nom (technique appelée masquage), ce qui permet d’utiliser une nouvelle valeur ou de modifier le type de la variable. Cela diffère de la mutabilité car chaque réutilisation du mot-clé let crée une nouvelle variable, sans modifier l'ancienne.

### B - Les types de données 
En Rust, chaque valeur a un type spécifique qui permet au compilateur de savoir comment traiter les données. Rust est langage statiquement typé, ce qui signifie qu’il doit connaître les types des variables à la compilation. Cependant, le compilateur peut déduire les types dans de nombreux cas, à moins qu'une clarification soit nécessaire
#### Type Scalaire
Les types scalaires représentent des valeurs uniques et sont divisés en quatre catégories principales :

- Entiers : Les entiers peuvent être signés (i) ou non signés (u), avec des tailles variant de 8 bits (i8, u8) à 128 bits (i128, u128). Le type entier par défaut en Rust est i32, suffisant pour la plupart des situations. Les entiers signés peuvent être négatifs, tandis que les non signés ne peuvent contenir que des valeurs positives.

- Flottants : Utilisés pour les nombres à virgule. Rust supporte les types f32 et f64, avec f64 comme choix par défaut car il est plus précis et aussi rapide que f32 sur la plupart des processeurs modernes.

- Booléens : Représentés par true ou false, ces valeurs booléennes sont principalement utilisées dans des structures conditionnelles comme if.

- Caractères : Le type char représente des caractères Unicode sur 4 octets, ce qui permet de manipuler des lettres, symboles et même des emojis.

#### Type Composés 
Les types composés regroupent plusieurs valeurs dans une seule entité. Rust offre deux types principaux :

- Tuples : Ils permettent de regrouper des valeurs de types différents dans un seul ensemble. Les tuples ont une taille fixe et ne peuvent pas être modifiés une fois déclarés. Chaque élément d'un tuple peut être accédé par son index ou déstructuré en variables distinctes.

- Tableaux : Contrairement aux tuples, tous les éléments d'un tableau doivent être du même type. Les tableaux ont également une taille fixe, ce qui les rend adaptés pour les situations où le nombre d'éléments est constant, comme une liste de mois de l'année.

### C - Les Fonctions
En Rust, les fonctions sont déclarées avec le mot-clé **fn**, suivi d'un nom, d'une liste de paramètres (facultative) et d'un corps de fonction entre accolades. Le langage utilise la convention snake case pour nommer les fonctions et les variables, c'est-à-dire en minuscules avec des tirets bas pour séparer les mots.
```Rust
fn main() {
    println!("Hello, world!");

    une_autre_fonction();
}
fn une_autre_fonction() {
    println!("Une autre fonction.");
}
```
Les fonctions peuvent être définies n'importe où dans le code, avant ou après main, tant qu'elles sont définies quelque part. Le programme exécute les instructions dans l'ordre où elles apparaissent.

#### Paramètres
Les fonctions peuvent accepter des paramètres, et vous devez toujours spécifier leur type.
```Rust
fn main() {
    afficher_mesure_avec_unite(5, 'h');
}
fn afficher_mesure_avec_unite(valeur: i32, unite: char) {
    println!("La mesure est : {}{}", valeur, unite);
}
```
Ici, la fonction prend deux paramètres (valeur et unite) et affiche les deux.

#### Instructions et expressions
En Rust, il est important de différencier instructions et expressions :

- Les instructions exécutent des actions mais ne retournent pas de valeur.
- Les expressions évaluent et retournent une valeur. 
```Rust
fn main() {
    let y = {
        let x = 3;
        x + 1
    };
    println!("La valeur de y est : {}", y); // y vaut 4
}
```
Ici, le bloc { let x = 3; x + 1 } est une expression qui retourne 4, affectée à y.

#### Fonctions avec valeurs de retour
Une fonction peut aussi retourner une valeur. Le type de retour est spécifié après une flèche **->**.<br>
La dernière expression de la fonction est sa valeur de retour, à moins que vous n'utilisiez explicitement return.
```Rust
fn cinq() -> i32 {
    5
}
fn main() {
    let x = cinq();
    println!("La valeur de x est : {}", x);
}
```
Ici, la fonction cinq retourne 5, et son type de retour est i32. Une fonction retourne implicitement la dernière expression si elle n'est pas suivie d'un point-virgule. Ajouter un point-virgule à une expression la transforme en instruction, ce qui peut provoquer des erreurs si un type de retour est attendu.
```Rust
fn main() {
    let x = plus_un(5);

    println!("La valeur de x est : {}", x);
}
fn plus_un(x: i32) -> i32 {
    x + 1;
}

$ cargo run
   Compiling functions v0.1.0 (file:///projects/functions)
error[E0308]: mismatched types
 --> src/main.rs:7:24
  |
7 | fn plus_un(x: i32) -> i32 {
  |    -------            ^^^ expected `i32`, found `()`
  |    |
  |    implicitly returns `()` as its body has no tail or `return` expression
8 |     x + 1;
  |          - help: consider removing this semicolon

For more information about this error, try `rustc --explain E0308`.
error: could not compile `functions` due to previous error

```
Si un point-virgule est ajouté après x + 1, cela génère une erreur, car cela empêche l'expression de retourner une valeur.

### D - Les Commentaires 
Les commentaires permettent d'ajouter des explications à votre code, sans être pris en compte par le compilateur. Ils aident les développeurs à rendre leur code plus lisible et compréhensible pour d'autres.<br>
- Les commentaires simples commencent par **//** et s'étendent jusqu'à la fin de la ligne.
- Pour les commentaires plus longs, vous ajoutez **//** sur chaque ligne
- Les commentaires peuvent aussi être ajoutés à la fin d'une ligne de code
- Il peuvent être aussi placé au -dessu de la ligne de code à laquelle ils se rapporte

```Rust
fn main() {
// hello, world
}
fn main() {
// Donc ici on fait quelque chose de compliqué, tellement long que nous avons
// besoin de plusieurs lignes de commentaires pour le faire ! Heureusement,
// ce commentaire va expliquer ce qui se passe.
}
fn main() {
    let nombre_chanceux = 7; // Je me sens chanceux aujourd'hui
}
fn main() {
    // Je me sens chanceux aujourd'hui
    let nombre_chanceux = 7;
}
 ```

Enfin, Rust propose aussi des commentaires de documentation, qui seront abordés plus tard.

### E - Les Structures de Contrôle
En Rust, les structures de contrôle vous permettent de diriger l'exécution de votre programme en fonction de conditions ou de boucler sur des actions répétées. Les principales structures de contrôle sont les expressions **if** et les boucles.

### Les expressions if
L'expression **if** vous permet d'exécuter du code en fonction d'une condition booléenne.<br> Si la condition est vraie, le bloc de code associé est exécuté, sinon, un bloc alternatif (avec else) peut être exécuté.
```Rust
fn main() {
    let nombre = 3;

    if nombre < 5 {
        println!("La condition est vérifiée");
    } else {
        println!("La condition n'est pas vérifiée");
    }
}
```
Dans cet exemple, si nombre est inférieur à 5, le premier bloc s'exécute, sinon c'est le second.

***Important*** : Les conditions **if** doivent toujours être de type booléen, sinon Rust renvoie une erreur de compilation. Par exemple, si vous essayez de tester un entier directement comme condition, Rust lèvera une erreur

#### Gérer plusieurs conditions avec else if

Si vous devez gérer plusieurs conditions, vous pouvez utiliser **else if** pour enchaîner plusieurs vérifications :
```Rust
fn main() {
    let nombre = 6;

    if nombre % 4 == 0 {
        println!("Le nombre est divisible par 4");
    } else if nombre % 3 == 0 {
        println!("Le nombre est divisible par 3");
    } else if nombre % 2 == 0 {
        println!("Le nombre est divisible par 2");
    } else {
        println!("Le nombre n'est pas divisible par 4, 3 ou 2");
    }
}
```
Le programme vérifie chaque condition dans l'ordre et exécute le premier bloc de code dont la condition est vraie.

#### Utiliser if dans une instruction let 
L'une des particularités de Rust est que if est une expression, ce qui signifie qu'il peut être utilisé pour affecter une variable directement.<br>
 Par exemple, vous pouvez affecter une variable en fonction d'une condition 
```Rust
fn main() {
    let condition = true;
    let nombre = if condition { 5 } else { 6 };

    println!("La valeur du nombre est : {}", nombre);
}
```
Dans cet exemple, la variable nombre recevra la valeur 5 si condition est vraie, sinon elle recevra la valeur 6.<br> Notez que les instructions if et else doivent retourner des valeurs du même type, sinon une erreur sera générée.

### Les répétitions avec les boucles
Rust propose plusieurs types de boucles pour exécuter un bloc de code plusieurs fois : **loop**, **while** et **for**.<br>Ces boucles vous permettent d'exécuter du code plusieurs fois jusqu'à ce qu'une condition soit remplie ou que vous décidiez de les arrêter.
#### Répéter du code avec loop
La boucle **loop** exécute un bloc de code en continu, créant une boucle infinie jusqu'à ce qu'une condition de sortie soit explicitement définie avec **break**.
```Rust
fn main() {
    loop {
        println!("À nouveau !");
    }
    //Ce programme affiche "Encore !" indéfiniment,
    //jusqu'à ce qu'il soit arrêté manuellement (par exemple, en appuyant sur ctrl-c).
}
$ cargo runCompiling loops v0.1.0 (file:///projects/loops)
    Finished dev [unoptimized + debuginfo] target(s) in 0.29s
     Running `target/debug/loops`
À nouveau !
À nouveau !
À nouveau !
À nouveau !
^CÀ nouveau !
```
Pour quitter une boucle, vous pouvez utiliser **break**.

Lorsque vous avez plusieurs boucles imbriquées, **break** et **continue** s'appliquent à la boucle la plus proche.<br> Vous pouvez aussi utiliser des étiquettes pour indiquer à quelle boucle le **break** ou **continue** s'appliquent.
```Rust
fn main() {
    let mut compteur = 0;
    'increment: loop {
        println!("compteur = {}", compteur);
        let mut restant = 10;

        loop {
            println!("restant = {}", restant);
            if restant == 9 {
                break;
            }
            if compteur == 2 {
                break 'increment;
            }
            restant -= 1;
        }

        compteur += 1;
    }
    println!("Fin du compteur = {}", compteur);
}
```
La boucle la plus à l'extérieur a l'étiquette increment, et elle va incrémenter de 0 à 2. <br>La boucle à l'intérieur n'a pas d'étiquette et va décrementer de 10 à 9. Le premier break qui ne précise pas d'étiquette va arrêter uniquement la boucle interne. L'instruction break 'increment; va arrêter la boucle la plus à l'extérieur.

### Retourner des valeurs d'une boucle
L'une des utilisations intéressantes d'une boucle **loop** est de réessayer une opération qui pourrait échouer ou qui dépend d'une condition externe pour se terminer.
Rust permet de retourner une valeur depuis une boucle loop. Vous pouvez le faire en plaçant l'expression que vous souhaitez renvoyer après le mot-clé break. Cette valeur sera alors accessible en dehors de la boucle et pourra être utilisée dans votre code
```Rust
fn main() {
    let mut compteur = 0;
    let resultat = loop {
        compteur += 1;

        if compteur == 10 {
            break compteur * 2;
        }
    };
    println!("Le résultat est {}", resultat);
}
```

### Les boucles conditionnelles avec while
Les boucles while sont couramment utilisées lorsqu'un programme doit répéter l'exécution d'un bloc de code tant qu'une condition reste vraie.<br> Lorsque la condition devient fausse, la boucle se termine, et le programme continue avec le reste du code.<br>
La structure d'une boucle while est très simple : tant que la condition spécifiée est vraie, le bloc de code associé est exécuté.<br> Dès que la condition est évaluée comme fausse, l'exécution sort de la boucle.
```Rust
fn main() {
    let mut nombre = 3;
    while nombre != 0 {
        println!("{} !", nombre);

        nombre -= 1;
    }
    println!("DÉCOLLAGE !!!");
}
```

### Boucler dans une collection avec for
Il est possible d'utiliser une boucle while pour parcourir les éléments d'une collection, comme un tableau. Cependant, cela peut être plus sujet à erreur.<br> Par exemple, si l'indice dépasse la taille du tableau, le programme peut paniquer.
```Rust
fn main() {
    let a = [10, 20, 30, 40, 50];
    let mut indice = 0;
    while indice < 5 {
        println!("La valeur est : {}", a[indice]);

        indice += 1;
    }
}
$ cargo run
   Compiling loops v0.1.0 (file:///projects/loops)
    Finished dev [unoptimized + debuginfo] target(s) in 0.32s
     Running `target/debug/loops`
La valeur est : 10
La valeur est : 20
La valeur est : 30
La valeur est : 40
La valeur est : 50
```

Bien que ce code fonctionne, il est plus propice aux erreurs et plus lent à cause des vérifications constantes de l'indice.<br>

Une alternative plus sûre et plus concise est d'utiliser la boucle for. Cette structure permet d'itérer automatiquement sur chaque élément de la collection sans se soucier des indices ou des dépassements.

```Rust
fn main() {
    let a = [10, 20, 30, 40, 50];
    for element in a {
        println!("La valeur est : {}", element);
    }
}
```
En utilisant for, le programme devient plus lisible et sûr.<br> Il n'est plus nécessaire de suivre manuellement les indices, et la boucle s'adapte automatiquement à la taille de la collection, ce qui élimine les risques de dépassement.

## Mes questions
Comment Rust s'intègre t-il dans d'autre langage ?<br>
Comment est gérer la mémoire en Rust ?<br>
Comment se differencie t-il des autres langages de programmation ?<br>
Expliquez en quoi Rust permet au développeur de corriger efficacement les erreurs.<br>
C'est quoi "un bogues de concurrence" ?<br>
Quelle sont les commande nécessaire lorsque l'on créer un projet via cargo ?<br>
Comment s'écrit un code en Rust et à quel langage ressemble t-il ?<br>
En quoi la mutabilité permet t'il d'avoir un code sûr ?<br>
Quel sont les principaux types en Rust ?<br>
Quel sont les deux types de données présent en Rust ? <br>
Quelle est la différence entre un tableau et un tuple en Rust <br>
Comment peuvent être retourné les valeurs ? <br>
Quel est la différence entre une boucle for et while ?<br>


###### Jonny MATHANARUBAN