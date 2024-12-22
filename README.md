# Documentation : Les méthodes magiques en PHP

Les méthodes magiques en PHP sont des méthodes spéciales qui commencent par `__` (double underscore). Elles permettent de définir des comportements personnalisés pour les objets. Voici une présentation simple des méthodes les plus couramment utilisées, avec des exemples clairs.

---


## 1. `__get($propriete)`

### Description :
Permet d'accéder à une propriété inaccessible ou inexistante d'un objet.

### Exemple :
```php
class Personne {
    private $age = 21;

    public function __get($propriete) {
        return "Propriété '{$propriete}' inaccessible.";
    }
}

$personne = new Personne();
echo $personne->age; // Affiche : Propriété 'age' inaccessible.
```

---

## 2. `__set($propriete, $valeur)`

### Description :
Permet de définir une valeur pour une propriété inaccessible ou inexistante.

### Exemple :
```php
class Personne {
    private $donnees = [];

    public function __set($propriete, $valeur) {
        $this->donnees[$propriete] = $valeur;
    }
}

$personne = new Personne();
$personne->nom = "Oumayma"; // Stocké dans $donnees
```

---

## 3. `__toString()`

### Description :
Définit le comportement lorsqu'un objet est converti en une chaîne de caractères (par exemple, avec `echo`).

### Exemple :
```php
class Personne {
    private $nom;

    public function __construct($nom) {
        $this->nom = $nom;
    }

    public function __toString() {
        return "Nom : {$this->nom}";
    }
}

$personne = new Personne("Oumayma");
echo $personne; // Affiche : Nom : Oumayma
```

---

## 4. `__call($nomMethode, $arguments)`

### Description :
Permet d'intercepter les appels à des méthodes inexistantes.

### Exemple :
```php
class Personne {
    public function __call($nomMethode, $arguments) {
        echo "Méthode '{$nomMethode}' non définie.";
    }
}

$personne = new Personne();
$personne->parler(); // Affiche : Méthode 'parler' non définie.
```

---

## 5. `__isset($propriete)`

### Description :
Définit le comportement lors de l'utilisation de `isset()` ou `empty()` sur une propriété inaccessible.

### Exemple :
```php
class Personne {
    private $donnees = ["nom" => "Oumayma"];

    public function __isset($propriete) {
        return isset($this->donnees[$propriete]);
    }
}

$personne = new Personne();
var_dump(isset($personne->nom)); // Affiche : bool(true)
```

---

## Conclusion

Les méthodes magiques permettent de personnaliser le comportement des objets en PHP de manière dynamique et intuitive. Cependant, elles doivent être utilisées avec précaution pour ne pas compliquer la lecture et le débogage du code.
