# 🦀 Rust : Typage, Immutabilité et `&`

Bienvenue dans l'univers de Rust ! 🚀 Aujourd'hui, on va voir trois concepts fondamentaux :  
📌 **Le typage**  
📌 **L'immutabilité**  
📌 **L'opérateur `&`**

## 🎨 1. Le Typage en Rust 🏛️

Rust est un langage **fortement typé**, ce qui signifie que chaque variable a un type bien défini et ne peut pas changer en cours de route.

🤨 Pourquoi ?  
✅ Pour éviter les erreurs inattendues ❌  
✅ Pour optimiser les performances 🚀  
✅ Pour mieux comprendre et structurer le code 🏧

**Exemple :**

```rust
let nombre: i32 = 42;  // un entier de 32 bits signé
let pi: f64 = 3.14;    // un nombre flottant 64 bits
let nom: &str = "Alice"; // une référence à une chaîne de caractères
```

💡 Rust peut souvent **déduire** le type automatiquement avec `let x = 10;` mais il est parfois utile de le préciser.

---

## 🔒 2. L'Immutabilité 🔐

En Rust, **les variables sont immuables par défaut**. Une fois assignée, une valeur ne peut pas être changée ! 😲

```rust
let age = 30;
age = 31; // ❌ Erreur : age est immuable !
```

🙌 Mais pourquoi ?  
✅ Ça évite les effets de bord et les bugs cachés 🐞  
✅ Ça aide le compilateur à optimiser le code 🚀

👉 **Si on veut modifier une variable**, il faut ajouter `mut` :

```rust
let mut age = 30;
age = 31; // ✅ Ça fonctionne !
```

---

## 🔢 3. L'Opérateur `&` : Les Références

En Rust, l'opérateur `&` permet de **créer une référence** à une variable sans en prendre la propriété.

💡 Ça permet :  
✅ D'éviter la copie des données ✅  
✅ De garder le contrôle sur qui peut modifier quoi 🏆

**Exemple :**

```rust
let x = 10;
let y = &x; // y est une référence vers x

println!("x = {}, y = {}", x, y); // 👍 Ça marche !
```

🔍 **Mais attention !** Les références mutables `&mut` ne peuvent être utilisées qu'une seule fois à la fois :

```rust
let mut z = 5;
let a = &mut z;
let b = &mut z; // ❌ Erreur ! Une seule référence mutable à la fois.
```

---

## 🔄 3. Le Casting : Conversion de Types

En Rust, il faut **convertir explicitement** un type vers un autre, car le compilateur ne fait pas de conversion automatique entre types numériques.

### 🔎 Exemple de Casting

```rust
let x: i32 = 10;
let y: f64 = x as f64 + 3.5; // Conversion explicite de i32 vers f64
println!("y = {}", y); // Affiche : y = 13.5
```

### 🏷️ Pourquoi utiliser `as` ?

✅ Pour éviter les erreurs d'incompatibilité entre types
✅ Pour assurer une conversion explicite et contrôlée

### 🌐 Attention aux pertes de données !

Si vous convertissez un `f64` en `i32`, la partie décimale est supprimée !

```rust
let a: f64 = 42.7;
let b: i32 = a as i32;
println!("b = {}", b); // Affiche : b = 42 (la partie .7 est perdue)
```

---

## 🌟 4. Les Chaînes de Caractères en Rust

Rust propose **deux types principaux** pour manipuler du texte :

- **`str`** : une **chaîne immuable** en dur dans la mémoire.
- **`String`** : une **chaîne dynamique** qui peut être modifiée.

### 🔄 Différences entre `str` et `String`

| Type     | Taille modifiable ? | Stockage               |
| -------- | ------------------- | ---------------------- |
| `str`    | Non ❌              | Sur la pile (stack) ✨ |
| `String` | Oui ✅              | Sur le tas (heap) 🏢   |

### 💡 Exemple avec `str`

```rust
fn afficher_message(msg: &str) {
    println!("Message : {}", msg);
}

let salut = "Bonjour";
afficher_message(salut); // 👍
```

### 🔍 Exemple avec `String`

```rust
let mut phrase = String::from("Hello");
phrase.push_str(", world!");
println!("{}", phrase); // Affiche : Hello, world!
```

### 🚀 Conversion entre `String` et `str`

Pour passer d'un `String` à un `&str` (référence vers un `str`), on utilise `as_str()` :

```rust
let s = String::from("Salut");
let s_slice: &str = s.as_str();
```

Pour passer de `&str` à `String`, on utilise `to_string()` ou `String::from()` :

```rust
let s1 = "Bonjour".to_string();
let s2 = String::from("Bonsoir");
```
