
### Cycle de Développement avec Tests (TDD - Test Driven Development)

#### Qu'est-ce que le TDD ?

Le **Test Driven Development (TDD)**, ou développement dirigé par les tests, est une approche de développement logiciel qui se concentre sur l'écriture de tests avant même de commencer à coder la fonctionnalité réelle. Cette méthode a été popularisée par Kent Beck, l'un des pionniers de l'Extreme Programming (XP). L'objectif principal du TDD est de garantir que le code écrit est toujours testé et que les nouvelles fonctionnalités sont intégrées sans introduire de bugs.

#### Pourquoi utiliser le TDD ?

- **Qualité du Code** : En écrivant les tests en premier, les développeurs sont contraints de penser à la manière dont le code sera utilisé. Cela conduit à un code plus propre et mieux structuré.
- **Réduction des Bugs** : Les tests écrits avant le code aident à identifier et corriger les bugs dès les premières phases du développement.
- **Confiance dans les Refactorisations** : Avec des tests en place, les développeurs peuvent refactoriser le code en toute confiance, sachant que les tests vérifieront que les modifications n'ont pas introduit de nouveaux bugs.
- **Documentation Vivante** : Les tests servent de documentation vivante sur le comportement attendu du code.

#### Le Cycle TDD Typique

Le cycle TDD typique est divisé en trois étapes principales, souvent appelées le cycle "rouge-vert-refactor". Voici une explication détaillée de chaque étape :

1. **Écrire un Test (Rouge)**
   - **Description** : La première étape consiste à écrire un test qui décrit une nouvelle fonctionnalité ou une amélioration du système. Ce test doit échouer puisqu'aucun code n'a encore été écrit pour implémenter cette fonctionnalité.
   - **Objectif** : Identifier ce qui doit être implémenté. Cela force le développeur à comprendre et à formaliser les exigences avant de commencer à coder.
   - **Exemple** : Supposons que vous développiez une calculatrice et que vous souhaitiez ajouter une fonctionnalité d'addition. Vous commenceriez par écrire un test qui vérifie que la méthode `add` retourne la somme de deux nombres.

     ```java
     // Fichier: CalculatorTest.java
     import static org.junit.jupiter.api.Assertions.assertEquals;
     import org.junit.jupiter.api.Test;

     public class CalculatorTest {
         @Test
         public void testAdd() {
             Calculator calculator = new Calculator();
             assertEquals(5, calculator.add(2, 3), "2 + 3 doit être égal à 5");
         }
     }
     ```

2. **Écrire le Code pour Faire Passer le Test (Vert)**
   - **Description** : Une fois le test écrit et exécuté (et constatant son échec), l'étape suivante consiste à écrire le code minimal nécessaire pour faire passer le test. L'objectif ici n'est pas d'écrire le code parfait, mais simplement de faire en sorte que le test passe.
   - **Objectif** : Implémenter la fonctionnalité de manière à ce que le test soit réussi.
   - **Exemple** : Après avoir écrit le test ci-dessus, vous implémenteriez la méthode `add` dans la classe `Calculator` pour qu'elle retourne la somme de deux nombres.

     ```java
     // Fichier: Calculator.java
     public class Calculator {
         public int add(int a, int b) {
             return a + b;
         }
     }
     ```

3. **Refactoriser le Code (Refactor)**
   - **Description** : Après avoir fait passer le test, l'étape suivante consiste à nettoyer et améliorer le code tout en s'assurant que tous les tests passent toujours. La refactorisation peut impliquer la simplification du code, l'amélioration de la lisibilité, ou la suppression de redondances.
   - **Objectif** : Améliorer la qualité du code sans modifier son comportement externe. Les tests existants garantissent que les modifications n'ont pas introduit de régressions.
   - **Exemple** : Dans cet exemple simple, il n'y aurait peut-être pas grand-chose à refactoriser. Mais dans des cas plus complexes, vous pourriez organiser votre code en méthodes plus petites, renommer des variables pour une meilleure clarté, ou éliminer du code dupliqué.



![image](https://github.com/yugmerabtene/DORANCO-2024-CDA-JUnit/assets/3670077/e8e0446f-636c-4adb-8094-95de8b790bac)

### Exemple Complet du Cycle TDD

Pour mieux illustrer le cycle TDD, reprenons l'exemple de la calculatrice avec une méthode `subtract` (soustraction).

1. **Écrire un Test (Rouge)**

   ```java
   // Fichier: CalculatorTest.java
   import static org.junit.jupiter.api.Assertions.assertEquals;
   import org.junit.jupiter.api.Test;

   public class CalculatorTest {
       @Test
       public void testAdd() {
           Calculator calculator = new Calculator();
           assertEquals(5, calculator.add(2, 3), "2 + 3 doit être égal à 5");
       }

       @Test
       public void testSubtract() {
           Calculator calculator = new Calculator();
           assertEquals(1, calculator.subtract(3, 2), "3 - 2 doit être égal à 1");
       }
   }
   ```

2. **Écrire le Code pour Faire Passer le Test (Vert)**

   ```java
   // Fichier: Calculator.java
   public class Calculator {
       public int add(int a, int b) {
           return a + b;
       }

       public int subtract(int a, int b) {
           return a - b;
       }
   }
   ```

3. **Refactoriser le Code (Refactor)**

   - Après avoir implémenté les méthodes `add` et `subtract`, supposons que vous vous rendiez compte que vous pouvez améliorer la lisibilité en ajoutant des commentaires ou en renommeant des variables pour plus de clarté.
   - **Avant la refactorisation :**

     ```java
     public class Calculator {
         public int add(int a, int b) {
             return a + b;
         }

         public int subtract(int a, int b) {
             return a - b;
         }
     }
     ```

   - **Après la refactorisation :**

     ```java
     public class Calculator {
         /**
          * Additionne deux entiers et retourne le résultat.
          *
          * @param a le premier entier
          * @param b le second entier
          * @return la somme de a et b
          */
         public int add(int a, int b) {
             return a + b;
         }

         /**
          * Soustrait le second entier du premier et retourne le résultat.
          *
          * @param a le premier entier
          * @param b le second entier
          * @return la différence entre a et b
          */
         public int subtract(int a, int b) {
             return a - b;
         }
     }
     ```

     ![image](https://github.com/yugmerabtene/DORANCO-2024-CDA-JUnit/assets/3670077/c26a7209-a8f6-4de9-aa54-d0eef77aa3ba)

### Importance des Tests Qui Échouent Initialement en TDD

En TDD (Test Driven Development), l'un des principes fondamentaux est de commencer par écrire des tests qui échouent. Voici pourquoi c'est important :

1. **Validation des Tests :** Lorsque vous écrivez un test avant d'implémenter le code, le test doit échouer pour prouver que le test est valide et qu'il détecte bien l'absence de la fonctionnalité. Si le test passe sans implémenter le code, cela signifie que le test n'est pas correctement écrit ou que la fonctionnalité testée est déjà présente (ce qui est rare dans TDD car on commence par les tests).
   
2. **Concentration sur les Exigences :** Écrire un test qui échoue vous force à vous concentrer sur les exigences et les spécifications exactes de la fonctionnalité avant d'écrire le code. Cela garantit que vous comprenez bien ce que le code doit accomplir.

3. **Feedback Immédiat :** Un test qui échoue fournit un feedback immédiat sur l'absence de la fonctionnalité. Ensuite, lorsque vous écrivez le code pour faire passer le test, vous obtenez une confirmation immédiate que votre code fonctionne comme prévu lorsque le test passe.

4. **Eviter les Faux Positifs :** Si vous écrivez d'abord le code et ensuite les tests, vous risquez d'écrire des tests qui passent uniquement parce qu'ils sont adaptés à votre implémentation, plutôt que parce qu'ils vérifient correctement la fonctionnalité attendue. En écrivant d'abord un test qui échoue, vous évitez ce piège.

### Exemple Illustré du Mini-Projet avec TDD

Reprenons notre projet de gestionnaire de bibliothèque et expliquons chaque étape en détaillant pourquoi les tests échouent initialement et comment ils guident le développement.

#### Étape 1 : Écriture des Tests (Rouge)

Nous écrivons les tests avant d'implémenter le code. Ces tests échoueront initialement car les fonctionnalités n'existent pas encore.

```java
// Fichier: LibraryManagerTest.java

import static org.junit.jupiter.api.Assertions.*;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;

/**
 * La classe LibraryManagerTest contient des tests unitaires pour la classe LibraryManager.
 */
public class LibraryManagerTest {
    private LibraryManager libraryManager;

    /**
     * Initialise un nouveau gestionnaire de bibliothèque avant chaque test.
     */
    @BeforeEach
    public void setUp() {
        libraryManager = new LibraryManager();
    }

    /**
     * Teste l'ajout d'un livre à la bibliothèque.
     */
    @Test
    public void testAddBook() {
        libraryManager.addBook("1984", "George Orwell");
        assertTrue(libraryManager.isBookAvailable("1984"), "Le livre doit être disponible après ajout");
    }

    /**
     * Teste l'emprunt d'un livre de la bibliothèque.
     */
    @Test
    public void testBorrowBook() {
        libraryManager.addBook("1984", "George Orwell");
        libraryManager.borrowBook("1984");
        assertFalse(libraryManager.isBookAvailable("1984"), "Le livre ne doit plus être disponible après emprunt");
    }

    /**
     * Teste le retour d'un livre à la bibliothèque.
     */
    @Test
    public void testReturnBook() {
        libraryManager.addBook("1984", "George Orwell");
        libraryManager.borrowBook("1984");
        libraryManager.returnBook("1984");
        assertTrue(libraryManager.isBookAvailable("1984"), "Le livre doit être disponible après retour");
    }

    /**
     * Teste la vérification de la disponibilité d'un livre.
     */
    @Test
    public void testIsBookAvailable() {
        libraryManager.addBook("1984", "George Orwell");
        assertTrue(libraryManager.isBookAvailable("1984"), "Le livre doit être disponible");
        libraryManager.borrowBook("1984");
        assertFalse(libraryManager.isBookAvailable("1984"), "Le livre ne doit plus être disponible");
    }
}
```

### Explication des Tests et Leur Échec Initial

1. **Test `testAddBook` :** 
   - **Action :** Ajoute un livre "1984" de George Orwell.
   - **Vérification :** Vérifie que le livre est disponible après ajout.
   - **Échec attendu :** Le test échoue car la méthode `addBook` n'est pas encore implémentée.

2. **Test `testBorrowBook` :** 
   - **Action :** Ajoute un livre, puis emprunte-le.
   - **Vérification :** Vérifie que le livre n'est plus disponible après emprunt.
   - **Échec attendu :** Le test échoue car la méthode `borrowBook` n'est pas encore implémentée.

3. **Test `testReturnBook` :** 
   - **Action :** Ajoute un livre, l'emprunte, puis le retourne.
   - **Vérification :** Vérifie que le livre est de nouveau disponible après retour.
   - **Échec attendu :** Le test échoue car la méthode `returnBook` n'est pas encore implémentée.

4. **Test `testIsBookAvailable` :** 
   - **Action :** Ajoute un livre, vérifie sa disponibilité, l'emprunte, puis vérifie sa disponibilité à nouveau.
   - **Vérification :** Vérifie que le livre est disponible après ajout et indisponible après emprunt.
   - **Échec attendu :** Le test échoue car la méthode `isBookAvailable` n'est pas encore implémentée.

### Étape 2 : Écriture du Code (Vert)

Maintenant que nous avons des tests qui échouent, nous pouvons implémenter le code pour faire passer ces tests.

```java
// Fichier: LibraryManager.java

import java.util.HashMap;
import java.util.Map;

/**
 * La classe LibraryManager gère une collection de livres, permettant d'ajouter, emprunter et retourner des livres.
 */
public class LibraryManager {
    private Map<String, Boolean> books;

    /**
     * Initialise un nouveau gestionnaire de bibliothèque.
     */
    public LibraryManager() {
        books = new HashMap<>();
    }

    /**
     * Ajoute un livre à la bibliothèque.
     *
     * @param title  le titre du livre
     * @param author l'auteur du livre
     */
    public void addBook(String title, String author) {
        books.put(title, true);
    }

    /**
     * Emprunte un livre de la bibliothèque.
     *
     * @param title le titre du livre à emprunter
     * @return true si le livre a été emprunté, false sinon
     */
    public boolean borrowBook(String title) {
        if (isBookAvailable(title)) {
            books.put(title, false);
            return true;
        }
        return false;
    }

    /**
     * Retourne un livre à la bibliothèque.
     *
     * @param title le titre du livre à retourner
     */
    public void returnBook(String title) {
        if (books.containsKey(title)) {
            books.put(title, true);
        }
    }

    /**
     * Vérifie si un livre est disponible à l'emprunt.
     *
     * @param title le titre du livre
     * @return true si le livre est disponible, false sinon
     */
    public boolean isBookAvailable(String title) {
        return books.getOrDefault(title, false);
    }
}
```

### Étape 3 : Refactorisation du Code (Refactor)

Après avoir fait passer les tests, nous pouvons améliorer et organiser le code si nécessaire. Dans ce cas, notre code est déjà assez simple et clair, donc peu de refactorisation est nécessaire. Nous allons ajouter quelques commentaires supplémentaires pour la clarté.

---
Rexplication plus clair ou cas ou vous ne coprenez pas le process : 


Le développement piloté par les tests (Test-Driven Development ou TDD) est une méthodologie de développement logiciel où les tests sont écrits avant le code de production. Cette approche se déroule en trois phases principales : rouge, vert, et refactorisation. Voici une explication détaillée de chacune de ces phases :

### Phase Rouge

1. **Écriture d'un test** :
    - Avant de commencer à écrire du code de production, un développeur écrit un test automatisé pour une fonctionnalité spécifique.
    - Ce test est généralement simple et se concentre sur une petite partie du comportement attendu du système.
    
2. **Exécution du test** :
    - Le test est exécuté immédiatement après avoir été écrit.
    - **But** : Le test doit échouer car le code de production n'est pas encore écrit. Cela confirme que le test est valide et qu'il détectera correctement l'absence de la fonctionnalité.

### Phase Verte

1. **Écriture du code minimal pour passer le test** :
    - Le développeur écrit juste assez de code de production pour faire passer le test.
    - Ce code n'est pas nécessairement bien structuré ou optimisé. L'objectif est simplement de passer de l'état "échec du test" à "succès du test".
    
2. **Exécution du test** :
    - Le test est exécuté à nouveau pour vérifier que la nouvelle implémentation le fait passer.
    - **But** : Le test doit réussir, ce qui prouve que le code écrit satisfait à la condition définie par le test.

### Phase de Refactorisation

1. **Nettoyage du code** :
    - Une fois que le test passe, le développeur améliore le code. Cela peut inclure la suppression de la duplication, la clarification de la logique, et l'application de bonnes pratiques de conception.
    
2. **Exécution des tests** :
    - Après avoir refactorisé, tous les tests (nouveaux et existants) doivent être exécutés pour s'assurer qu'aucun comportement n'a été involontairement modifié.
    - **But** : Maintenir la qualité du code sans introduire de régressions.

### Pourquoi les tests doivent échouer initialement ?

1. **Validation du test** :
    - Un test qui échoue initialement prouve qu'il est valide et qu'il détecte effectivement l'absence de la fonctionnalité.
    
2. **Motivation pour écrire du code** :
    - Un test qui échoue fournit une motivation immédiate et spécifique pour écrire le code nécessaire pour faire passer ce test.

3. **Prévention de faux positifs** :
    - Si un test réussit immédiatement, il se peut qu'il ne soit pas correctement configuré ou qu'il ne teste pas réellement la fonctionnalité prévue.

4. **Cycle de feedback rapide** :
    - En commençant par un test qui échoue, le développeur bénéficie d'un cycle de feedback rapide, facilitant la détection et la correction des erreurs dès les premières étapes du développement.

### Exemple Pratique

1. **Phase Rouge** :
    - Écrire un test : `assert add(1, 1) == 2`
    - Exécution : Le test échoue car la fonction `add` n'est pas définie.

2. **Phase Verte** :
    - Écrire le code : `def add(a, b): return a + b`
    - Exécution : Le test passe.

3. **Refactorisation** :
    - Améliorer le code si nécessaire, par exemple, ajouter des validations ou simplifier la logique.
    - Exécution : Tous les tests passent.

