Bien sûr, je vais structurer et détailler davantage le module "JUnit dans IntelliJ IDEA" avec des explications claires et numérotées pour faciliter la compréhension. Voici la version améliorée et bien structurée du module :

---

# Module-01 : Configuration et Utilisation de JUnit dans IntelliJ IDEA

## Introduction

JUnit est un framework de tests unitaires pour le langage de programmation Java. Il vous permet de tester des unités de code de manière isolée pour s'assurer de leur bon fonctionnement. Ce module vous guidera à travers l'installation de JUnit dans IntelliJ IDEA, l'écriture et l'exécution de tests unitaires, ainsi que l'utilisation de pratiques avancées comme le mocking avec Mockito et l'analyse de couverture de code avec JaCoCo.

## Configuration de JUnit dans IntelliJ IDEA

Pour écrire et exécuter des tests unitaires avec JUnit dans IntelliJ IDEA, suivez ces étapes :

### Étape 1 : Installer IntelliJ IDEA

1. **Télécharger et installer IntelliJ IDEA**
   - Téléchargez IntelliJ IDEA depuis le [site officiel](https://www.jetbrains.com/idea/download/).
   - Installez IntelliJ IDEA en suivant les instructions spécifiques à votre système d'exploitation.

### Étape 2 : Créer un nouveau projet

2. **Créer un nouveau projet**
   - Ouvrez IntelliJ IDEA.
   - Cliquez sur `File` > `New` > `Project`.
   - Sélectionnez `Java` dans la liste des types de projet.
   - Donnez un nom à votre projet et choisissez un emplacement.
   - Cliquez sur `Finish`.

### Étape 3 : Ajouter JUnit à votre projet

3. **Ajouter JUnit à votre projet**
   - Cliquez sur `File` > `Project Structure` ou utilisez le raccourci `Ctrl+Alt+Shift+S`.
   - Dans la section `Libraries`, cliquez sur le signe `+` pour ajouter une nouvelle bibliothèque.
   - Sélectionnez `From Maven...`.
   - Dans la boîte de dialogue qui s'affiche, tapez `junit:junit:4.13.2` (ou une version plus récente si disponible).
   - Cliquez sur `OK` et IntelliJ téléchargera et ajoutera JUnit à votre projet.

## Écrire et Exécuter des Tests Unitaires avec JUnit

Pour illustrer l'importance des tests unitaires, nous allons créer différents exercices correspondant à des avantages spécifiques des tests unitaires.

### 1. Détection Précoce des Erreurs

**But :** Les tests unitaires permettent de détecter les erreurs dès les premières phases du développement, réduisant ainsi les coûts et le temps nécessaires pour corriger les bugs.

**Exercice associé :** Créer une méthode simple et écrire des tests pour elle, montrant comment les tests peuvent immédiatement identifier les erreurs de logique.

#### Exemple :

1. **Créer la classe `Calculator` avec une méthode `add` :**

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

2. **Créer la classe de test `CalculatorTest` :**

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

### 2. Code de Meilleure Qualité

**But :** En écrivant des tests, les développeurs sont encouragés à écrire du code plus propre et mieux structuré.

**Exercice associé :** Créer une classe avec des méthodes simples, puis écrire des tests unitaires pour encourager la bonne structuration et la clarté du code.

#### Exemple :

1. **Créer la classe `Person` :**

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

2. **Créer la classe de test `PersonTest` :**

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

### 3. Refactorisation Facilitée

**But :** Les tests unitaires permettent de refactoriser le code en toute confiance, sachant que les tests vérifieront que les fonctionnalités restent intactes.

**Exercice associé :** Refactoriser une méthode existante pour inclure une nouvelle logique (par exemple, la vérification des valeurs nulles), puis écrire des tests unitaires pour garantir que les changements n'introduisent pas de nouveaux bugs.

#### Exemple :

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

### 4. Documentation Vivante

**But :** Les tests peuvent servir de documentation sur le comportement attendu du code.

**Exercice associé :** Créer des méthodes de classe avec des comportements spécifiques (comme dépôt et retrait d'argent dans un compte bancaire), puis écrire des tests unitaires détaillés pour documenter ces comportements.

#### Exemple :

1. **Créer la classe `BankAccount` :**

   ```java
   // Fichier: BankAccount.java
   /**
    * La classe BankAccount représente un compte bancaire avec des méthodes pour déposer, retirer et transférer des fonds.
    */
   public class BankAccount {
       private double

 balance;

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

2. **Créer la classe de test `BankAccountTest` :**

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

### 5. Réduction des Régressions

**But :** Les tests unitaires permettent de vérifier que les nouvelles modifications n'ont pas introduit de nouvelles erreurs.

**Exercice associé :** Ajouter de nouvelles fonctionnalités à une classe existante (comme le transfert d'argent entre comptes), puis écrire des tests unitaires pour s'assurer que les nouvelles fonctionnalités fonctionnent correctement et que les anciennes fonctionnalités ne sont pas brisées.

#### Exemple :

1. **Ajouter la méthode `transfer` dans la classe `BankAccount` :**

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

2. **Mettre à jour les tests dans `BankAccountTest` :**

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

## Outils et Pratiques Recommandées

### Partie 1 : Utilisation de Mocking avec Mockito

Mockito est un framework de mock permettant de simuler des objets dans vos tests unitaires, ce qui est très utile pour isoler les unités de code et tester leur comportement de manière plus précise.

#### Configuration de Mockito dans IntelliJ IDEA

1. **Ajouter les dépendances Mockito :**

   Ajoutez les dépendances Mockito à votre fichier `pom.xml` (pour Maven) ou `build.gradle` (pour Gradle).

   **Pour Maven :**

   ```xml
   <dependency>
       <groupId>org.mockito</groupId>
       <artifactId>mockito-core</artifactId>
       <version>4.8.0</version>
       <scope>test</scope>
   </dependency>
   ```

   **Pour Gradle :**

   ```groovy
   testImplementation 'org.mockito:mockito-core:4.8.0'
   ```

2. **Écrire un test utilisant Mockito :**

   Supposons que vous ayez une classe `UserService` qui dépend d'un `UserRepository`. Vous pouvez utiliser Mockito pour mocker `UserRepository` dans vos tests.

   ```java
   // Fichier: UserServiceTest.java
   import static org.mockito.Mockito.*;
   import static org.junit.jupiter.api.Assertions.*;
   import org.junit.jupiter.api.Test;
   import org.mockito.Mockito;

   public class UserServiceTest {
       @Test
       public void testGetUserById() {
           UserRepository mockRepo = mock(UserRepository.class);
           UserService userService = new UserService(mockRepo);

           User mockUser = new User("John", "Doe");
           when(mockRepo.findById(1)).thenReturn(mockUser);

           User result = userService.getUserById(1);
           assertEquals("John Doe", result.getFullName());
       }
   }
   ```

### Partie 2 : Coverage des Tests avec JaCoCo

JaCoCo est un outil de couverture de code qui vous aide à voir quelles parties de votre code sont couvertes par des tests et lesquelles ne le sont pas.

#### Configuration de JaCoCo dans IntelliJ IDEA

1. **Ajouter les dépendances JaCoCo :**

   Ajoutez JaCoCo à votre fichier `

pom.xml` (pour Maven) ou `build.gradle` (pour Gradle).

   **Pour Maven :**

   ```xml
   <plugin>
       <groupId>org.jacoco</groupId>
       <artifactId>jacoco-maven-plugin</artifactId>
       <version>0.8.8</version>
       <executions>
           <execution>
               <goals>
                   <goal>prepare-agent</goal>
               </goals>
           </execution>
           <execution>
               <id>report</id>
               <phase>test</phase>
               <goals>
                   <goal>report</goal>
               </goals>
           </execution>
       </executions>
   </plugin>
   ```

   **Pour Gradle :**

   ```groovy
   plugins {
       id 'jacoco'
   }

   jacoco {
       toolVersion = '0.8.8'
   }

   test {
       finalizedBy jacocoTestReport
   }

   jacocoTestReport {
       reports {
           xml.enabled true
           html.enabled true
       }
   }
   ```

2. **Analyser la couverture des tests :**

   Exécutez vos tests et générez le rapport de couverture.

   **Avec Maven :**

   ```bash
   mvn clean test
   mvn jacoco:report
   ```

   **Avec Gradle :**

   ```bash
   ./gradlew test jacocoTestReport
   ```

3. **Visualiser les résultats :**

   Ouvrez le fichier `target/site/jacoco/index.html` pour voir le rapport de couverture ou le dossier `build/reports/jacoco/test/html/index.html` pour Gradle. Vous y verrez les classes et méthodes couvertes et non couvertes par vos tests.

### Exemples Complétés

#### Test avec Mocking

```java
// Fichier: UserServiceTest.java
import static org.mockito.Mockito.*;
import static org.junit.jupiter.api.Assertions.*;
import org.junit.jupiter.api.Test;
import org.mockito.Mockito;

public class UserServiceTest {
    @Test
    public void testGetUserById() {
        UserRepository mockRepo = mock(UserRepository.class);
        UserService userService = new UserService(mockRepo);

        User mockUser = new User("John", "Doe");
        when(mockRepo.findById(1)).thenReturn(mockUser);

        User result = userService.getUserById(1);
        assertEquals("John Doe", result.getFullName());
    }
}
```

#### Test avec Coverage JaCoCo

```java
// Fichier: BankAccountTest.java
import static org.junit.jupiter.api.Assertions.*;
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

