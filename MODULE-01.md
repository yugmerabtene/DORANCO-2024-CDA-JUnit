### Configuration de JUnit dans IntelliJ IDEA

#### Étape 1: Installer IntelliJ IDEA

1. **Télécharger et installer IntelliJ IDEA:**
   - Téléchargez IntelliJ IDEA depuis le [site officiel](https://www.jetbrains.com/idea/download/).
   - Installez IntelliJ IDEA en suivant les instructions spécifiques à votre système d'exploitation.

#### Étape 2: Créer un nouveau projet

1. **Créer un nouveau projet:**
   - Ouvrez IntelliJ IDEA.
   - Cliquez sur `File` > `New` > `Project`.
   - Sélectionnez `Java` dans la liste des types de projet.
   - Donnez un nom à votre projet et choisissez un emplacement.
   - Cliquez sur `Finish`.

#### Étape 3: Ajouter JUnit à votre projet

1. **Ajouter JUnit à votre projet:**
   - Cliquez sur `File` > `Project Structure` ou utilisez le raccourci `Ctrl+Alt+Shift+S`.
   - Dans la section `Libraries`, cliquez sur le signe `+` pour ajouter une nouvelle bibliothèque.
   - Sélectionnez `From Maven...`.
   - Dans la boîte de dialogue qui s'affiche, tapez `junit:junit:4.13.2` (ou une version plus récente si disponible).
   - Cliquez sur `OK` et IntelliJ téléchargera et ajoutera JUnit à votre projet.

### Écriture de Tests Unitaires Simples

#### Partie 1: Structure d'un test unitaire

##### Méthodes de test

Les méthodes de test sont les blocs de construction de vos tests unitaires. Elles contiennent le code qui vérifie si une unité de code (par exemple, une méthode) fonctionne comme prévu. En JUnit, une méthode de test est simplement une méthode Java marquée avec l'annotation `@Test`.

##### Annotations

Les annotations jouent un rôle crucial dans la configuration et l'exécution des tests unitaires. Voici les principales annotations utilisées en JUnit :

- **`@Test`**: Indique que la méthode annotée est une méthode de test.
- **`@BeforeEach`**: Indique qu'une méthode doit être exécutée avant chaque méthode de test.
- **`@AfterEach`**: Indique qu'une méthode doit être exécutée après chaque méthode de test.
- **`@BeforeAll`**: Indique qu'une méthode statique doit être exécutée une seule fois avant l'exécution de toutes les méthodes de test de la classe.
- **`@AfterAll`**: Indique qu'une méthode statique doit être exécutée une seule fois après l'exécution de toutes les méthodes de test de la classe.

##### Exemple

1. **Structure d'un test unitaire avec annotations:**

   ```java
   import org.junit.jupiter.api.*;

   public class ExampleTest {
       
       @BeforeAll
       public static void setupClass() {
           // Exécuté une fois avant tous les tests
           System.out.println("Avant tous les tests");
       }

       @BeforeEach
       public void setup() {
           // Exécuté avant chaque test
           System.out.println("Avant chaque test");
       }

       @Test
       public void testExample() {
           // Exécution du test
           Assertions.assertTrue(true, "Ce test réussira toujours");
       }

       @AfterEach
       public void tearDown() {
           // Exécuté après chaque test
           System.out.println("Après chaque test");
       }

       @AfterAll
       public static void tearDownClass() {
           // Exécuté une fois après tous les tests
           System.out.println("Après tous les tests");
       }
   }
   ```

#### Partie 2: Assertions de base

Les assertions sont utilisées pour vérifier que les résultats attendus et réels d'un test sont les mêmes. JUnit fournit plusieurs méthodes d'assertion pour faciliter cette vérification.

##### Principales méthodes d'assertion

- **`assertEquals(expected, actual)`**: Vérifie que les deux valeurs sont égales.
- **`assertTrue(condition)`**: Vérifie que la condition est vraie.
- **`assertFalse(condition)`**: Vérifie que la condition est fausse.
- **`assertNull(object)`**: Vérifie que l'objet est null.
- **`assertNotNull(object)`**: Vérifie que l'objet n'est pas null.
- **`assertThrows(expectedType, executable)`**: Vérifie qu'une exception de type attendu est lancée.

##### Exemple

1. **Exemple d'utilisation des assertions de base:**

   ```java
   import org.junit.jupiter.api.Test;
   import static org.junit.jupiter.api.Assertions.*;

   public class AssertionsTest {
       
       @Test
       public void testAssertions() {
           assertEquals(4, 2 + 2, "2 + 2 doit être égal à 4");
           assertTrue(3 > 2, "3 est supérieur à 2");
           assertFalse(3 < 2, "3 n'est pas inférieur à 2");
           assertNull(null, "Cet objet doit être null");
           assertNotNull(new Object(), "Cet objet ne doit pas être null");
       }

       @Test
       public void testException() {
           assertThrows(ArithmeticException.class, () -> {
               int result = 1 / 0;
           }, "Diviser par zéro doit lancer ArithmeticException");
       }
   }
   ```

#### Partie 3: Tests de méthodes simples et avec exceptions

Dans cette section, nous allons écrire des tests unitaires pour des méthodes simples ainsi que des méthodes qui lancent des exceptions.

##### Exemple

1. **Test de méthodes simples:**

   ```java
   public class SimpleMath {
       public int add(int a, int b) {
           return a + b;
       }

       public int subtract(int a, int b) {
           return a - b;
       }
   }

   // Fichier: SimpleMathTest.java
   import org.junit.jupiter.api.Test;
   import static org.junit.jupiter.api.Assertions.*;

   public class SimpleMathTest {

       @Test
       public void testAdd() {
           SimpleMath math = new SimpleMath();
           assertEquals(5, math.add(2, 3), "2 + 3 doit être égal à 5");
       }

       @Test
       public void testSubtract() {
           SimpleMath math = new SimpleMath();
           assertEquals(1, math.subtract(3, 2), "3 - 2 doit être égal à 1");
       }
   }
   ```

2. **Test de méthodes avec exceptions:**

   ```java
   public class Calculator {
       public int divide(int a, int b) {
           if (b == 0) {
               throw new ArithmeticException("Division par zéro");
           }
           return a / b;
       }
   }

   // Fichier: CalculatorTest.java
   import org.junit.jupiter.api.Test;
   import static org.junit.jupiter.api.Assertions.*;

   public class CalculatorTest {

       @Test
       public void testDivide() {
           Calculator calculator = new Calculator();
           assertEquals(2, calculator.divide(4, 2), "4 / 2 doit être égal à 2");
       }

       @Test
       public void testDivideByZero() {
           Calculator calculator = new Calculator();
           assertThrows(ArithmeticException.class, () -> {
               calculator.divide(4, 0);
           }, "Diviser par zéro doit lancer ArithmeticException");
       }
   }
   ```

### 1. Détection précoce des erreurs

**But :** Les tests unitaires permettent de détecter les erreurs dès les premières phases du développement, réduisant ainsi les coûts et le temps nécessaires pour corriger les bugs.

**Exercice associé :** Créer une méthode simple et écrire des tests pour elle, montrant comment les tests peuvent immédiatement identifier les erreurs de logique.

#### Exemple

1. **Créer la classe `Calculator` avec une méthode `add`:**

   ```java
   // Fichier: Calculator.java
   /**
    * La classe Calculator contient des méthodes pour effectuer des opérations arithmétiques de base.
    */
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
   }
   ```

2. **Créer la classe de test `CalculatorTest`:**

   ```java
   // Fichier: CalculatorTest.java
   import static org.junit.jupiter.api.Assertions.assertEquals;
   import org.junit.jupiter.api.Test;

   /**
    * La classe CalculatorTest contient des tests unitaires pour la classe Calculator.
    */
   public class CalculatorTest {
       /**
        * Teste la méthode add pour vérifier que les valeurs sont correctement additionnées.
        */
       @Test
       public void testAdd() {
           Calculator calculator = new Calculator();
           assertEquals(5, calculator.add(2, 3), "2 + 3 doit être égal à 5");
           assertEquals(0, calculator.add(0, 0), "0 + 0 doit être égal à 0");
           assertEquals(-5, calculator.add(-2, -3), "-2 + -3 doit être égal à -5");
       }
   }
   ```

### 2. Code de meilleure qualité

**But :** En écrivant des tests, les développeurs sont encouragés à écrire du code plus propre et mieux structuré.

**Exercice associé :** Créer une classe avec des méthodes simples, puis écrire des tests unitaires pour encourager la bonne structuration et la clarté du code.



#### Exemple

1. **Créer la classe `Person`:**

   ```java
   // Fichier: Person.java
   /**
    * La classe Person représente une personne avec un prénom et un nom de famille.
    */
   public class Person {
       private String firstName;
       private String lastName;

       /**
        * Constructeur pour initialiser une personne avec un prénom et un nom de famille.
        *
        * @param firstName le prénom
        * @param lastName le nom de famille
        */
       public Person(String firstName, String lastName) {
           this.firstName = firstName;
           this.lastName = lastName;
       }

       /**
        * Retourne le nom complet de la personne.
        *
        * @return le prénom et le nom de famille concaténés
        */
       public String getFullName() {
           return firstName + " " + lastName;
       }
   }
   ```

2. **Créer la classe de test `PersonTest`:**

   ```java
   // Fichier: PersonTest.java
   import static org.junit.jupiter.api.Assertions.assertEquals;
   import org.junit.jupiter.api.Test;

   /**
    * La classe PersonTest contient des tests unitaires pour la classe Person.
    */
   public class PersonTest {
       /**
        * Teste la méthode getFullName pour vérifier que le nom complet est correct.
        */
       @Test
       public void testGetFullName() {
           Person person = new Person("John", "Doe");
           assertEquals("John Doe", person.getFullName(), "Le nom complet doit être 'John Doe'");

           Person person2 = new Person("Jane", "Smith");
           assertEquals("Jane Smith", person2.getFullName(), "Le nom complet doit être 'Jane Smith'");
       }
   }
   ```

### 3. Refactorisation facilitée

**But :** Les tests unitaires permettent de refactoriser le code en toute confiance, sachant que les tests vérifieront que les fonctionnalités restent intactes.

**Exercice associé :** Refactoriser une méthode existante pour inclure une nouvelle logique (par exemple, la vérification des valeurs nulles), puis écrire des tests unitaires pour garantir que les changements n'introduisent pas de nouveaux bugs.

#### Exemple

1. **Refactoriser la méthode `add` de `Calculator` pour inclure une vérification des valeurs nulles :**

   ```java
   // Fichier: Calculator.java
   public class Calculator {
       /**
        * Additionne deux entiers et retourne le résultat. Lève une exception si un des arguments est null.
        *
        * @param a le premier entier (ne doit pas être null)
        * @param b le second entier (ne doit pas être null)
        * @return la somme de a et b
        * @throws IllegalArgumentException si a ou b est null
        */
       public int add(Integer a, Integer b) {
           if (a == null || b == null) {
               throw new IllegalArgumentException("Les arguments ne doivent pas être nuls");
           }
           return a + b;
       }
   }
   ```

2. **Mettre à jour les tests dans `CalculatorTest` pour vérifier la nouvelle logique :**

   ```java
   // Fichier: CalculatorTest.java
   import static org.junit.jupiter.api.Assertions.assertEquals;
   import static org.junit.jupiter.api.Assertions.assertThrows;
   import org.junit.jupiter.api.Test;

   public class CalculatorTest {
       @Test
       public void testAdd() {
           Calculator calculator = new Calculator();
           assertEquals(5, calculator.add(2, 3), "2 + 3 doit être égal à 5");
           assertEquals(0, calculator.add(0, 0), "0 + 0 doit être égal à 0");
           assertEquals(-5, calculator.add(-2, -3), "-2 + -3 doit être égal à -5");
       }

       @Test
       public void testAddWithNull() {
           Calculator calculator = new Calculator();
           assertThrows(IllegalArgumentException.class, () -> {
               calculator.add(null, 2);
           }, "Les arguments ne doivent pas être nuls");
           assertThrows(IllegalArgumentException.class, () -> {
               calculator.add(2, null);
           }, "Les arguments ne doivent pas être nuls");
       }
   }
   ```

### 4. Documentation vivante

**But :** Les tests peuvent servir de documentation sur le comportement attendu du code.

**Exercice associé :** Créer des méthodes de classe avec des comportements spécifiques (comme dépôt et retrait d'argent dans un compte bancaire), puis écrire des tests unitaires détaillés pour documenter ces comportements.

#### Exemple

1. **Créer la classe `BankAccount`:**

   ```java
   // Fichier: BankAccount.java
   /**
    * La classe BankAccount représente un compte bancaire avec des méthodes pour déposer, retirer et transférer des fonds.
    */
   public class BankAccount {
       private double balance;

       /**
        * Constructeur pour initialiser le compte bancaire avec un solde initial.
        *
        * @param initialBalance le solde initial
        * @throws IllegalArgumentException si le solde initial est négatif
        */
       public BankAccount(double initialBalance) {
           if (initialBalance < 0) {
               throw new IllegalArgumentException("Le solde initial ne peut pas être négatif");
           }
           this.balance = initialBalance;
       }

       /**
        * Dépose un montant sur le compte bancaire.
        *
        * @param amount le montant à déposer
        * @throws IllegalArgumentException si le montant est négatif ou zéro
        */
       public void deposit(double amount) {
           if (amount <= 0) {
               throw new IllegalArgumentException("Le montant du dépôt doit être positif");
           }
           balance += amount;
       }

       /**
        * Retire un montant du compte bancaire.
        *
        * @param amount le montant à retirer
        * @throws IllegalArgumentException si les fonds sont insuffisants
        */
       public void withdraw(double amount) {
           if (amount > balance) {
               throw new IllegalArgumentException("Fonds insuffisants");
           }
           balance -= amount;
       }

       /**
        * Transfère un montant d'un compte bancaire à un autre.
        *
        * @param toAccount le compte vers lequel transférer les fonds
        * @param amount le montant à transférer
        */
       public void transfer(BankAccount toAccount, double amount) {
           this.withdraw(amount);
           toAccount.deposit(amount);
       }

       /**
        * Retourne le solde actuel du compte bancaire.
        *
        * @return le solde actuel
        */
       public double getBalance() {
           return balance;
       }
   }
   ```

2. **Créer la classe de test `BankAccountTest`:**

   ```java
   // Fichier: BankAccountTest.java
   import static org.junit.jupiter.api.Assertions.assertEquals;
   import static org.junit.jupiter.api.Assertions.assertThrows;
   import org.junit.jupiter.api.Test;

   /**
    * La classe BankAccountTest contient des tests unitaires pour la classe BankAccount.
    */
   public class BankAccountTest {
       @Test
       public void testInitialBalance() {
           BankAccount account = new BankAccount(100.0);
           assertEquals(100.0, account.getBalance(), "Le solde initial doit être de 100.0");
       }

       @Test
       public void testDeposit() {
           BankAccount account = new BankAccount(100.0);
           account.deposit(50.0);
           assertEquals(150.0, account.getBalance(), "Le solde après dépôt doit être de 150.0");
       }

       @Test
       public void testWithdraw() {
           BankAccount account = new BankAccount(100.0);
           account.withdraw(50.0);
           assertEquals(50.0, account.getBalance(), "Le solde après retrait doit être de 50.0");
       }

       @Test
       public void testWithdrawInsufficientFunds() {
           BankAccount account = new BankAccount(100.0);
           assertThrows(IllegalArgumentException.class, () -> {
               account.withdraw(150.0);
           }, "Un retrait de 150.0 devrait déclencher une exception de fonds insuffisants");
       }

       @Test
       public void testTransfer() {
           BankAccount account1 = new BankAccount(100.0);
           BankAccount account2 = new BankAccount(50.0);
           account1.transfer(account2, 30.0);
           assertEquals(70.0, account1.getBalance(), "Le solde après transfert doit être de 70.0 pour le compte 1");
           assertEquals(80.0, account2.getBalance(), "Le solde après transfert doit être de 80.0 pour le compte 2");
       }
   }
   ```

### 5. Réduction des régressions

**But :** Les tests unitaires permettent de vérifier que les nouvelles modifications n'ont pas introduit de nouvelles erreurs.

**Exercice associé :** Ajouter de nouvelles fonctionnalités à une classe existante (comme le transfert d'argent entre comptes), puis écrire des tests unitaires pour s'assurer que les nouvelles fonctionnalités fonctionnent correctement et que les anciennes fonctionnalités ne sont pas brisées.

#### Exemple

1. **Ajouter la méthode `transfer` dans la classe `BankAccount`:**

   ```java
   // Fichier: BankAccount.java
   public class BankAccount {
       private double balance;

       public BankAccount(double initialBalance) {
           if (initialBalance < 0) {
               throw new IllegalArgumentException("Le solde initial ne peut pas être négatif");
           }
          

 this.balance = initialBalance;
       }

       public void deposit(double amount) {
           if (amount <= 0) {
               throw new IllegalArgumentException("Le montant du dépôt doit être positif");
           }
           balance += amount;
       }

       public void withdraw(double amount) {
           if (amount > balance) {
               throw new IllegalArgumentException("Fonds insuffisants");
           }
           balance -= amount;
       }

       public void transfer(BankAccount toAccount, double amount) {
           this.withdraw(amount);
           toAccount.deposit(amount);
       }

       public double getBalance() {
           return balance;
       }
   }
   ```

2. **Mettre à jour les tests dans `BankAccountTest`:**

   ```java
   // Fichier: BankAccountTest.java
   import static org.junit.jupiter.api.Assertions.assertEquals;
   import static org.junit.jupiter.api.Assertions.assertThrows;
   import org.junit.jupiter.api.Test;

   public class BankAccountTest {
       @Test
       public void testInitialBalance() {
           BankAccount account = new BankAccount(100.0);
           assertEquals(100.0, account.getBalance(), "Le solde initial doit être de 100.0");
       }

       @Test
       public void testDeposit() {
           BankAccount account = new BankAccount(100.0);
           account.deposit(50.0);
           assertEquals(150.0, account.getBalance(), "Le solde après dépôt doit être de 150.0");
       }

       @Test
       public void testWithdraw() {
           BankAccount account = new BankAccount(100.0);
           account.withdraw(50.0);
           assertEquals(50.0, account.getBalance(), "Le solde après retrait doit être de 50.0");
       }

       @Test
       public void testWithdrawInsufficientFunds() {
           BankAccount account = new BankAccount(100.0);
           assertThrows(IllegalArgumentException.class, () -> {
               account.withdraw(150.0);
           }, "Un retrait de 150.0 devrait déclencher une exception de fonds insuffisants");
       }

       @Test
       public void testTransfer() {
           BankAccount account1 = new BankAccount(100.0);
           BankAccount account2 = new BankAccount(50.0);
           account1.transfer(account2, 30.0);
           assertEquals(70.0, account1.getBalance(), "Le solde après transfert doit être de 70.0 pour le compte 1");
           assertEquals(80.0, account2.getBalance(), "Le solde après transfert doit être de 80.0 pour le compte 2");
       }
   }
   ```
