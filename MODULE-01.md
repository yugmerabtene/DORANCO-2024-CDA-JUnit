# Module-01 : Configuration et Utilisation de JUnit dans IntelliJ IDEA

## Durée : 8 heures

## Objectifs :

- Comprendre les bases des tests unitaires
- Introduction à JUnit
- Écrire des tests unitaires simples

## Contenu :

### Introduction aux Tests Unitaires (2 heures)

#### Partie 1 : Importance des tests unitaires (1 heure)

1. **Pourquoi tester ?**
   - Les tests unitaires permettent de s'assurer que le code fonctionne comme prévu.
   - Ils aident à identifier les bugs tôt dans le cycle de développement, ce qui réduit le coût et le temps nécessaires pour les corriger.
   - Les tests unitaires facilitent la maintenance du code en permettant de vérifier que les modifications n'introduisent pas de régressions.



#### Partie 2 : Principes de base des tests unitaires (1 heure)

1. **Définitions et concepts**
   - Un test unitaire est un test qui vérifie le fonctionnement d'une petite unité de code (comme une méthode ou une classe).
   - Les tests unitaires doivent être automatisés et rapides à exécuter.
   - Ils doivent être indépendants les uns des autres pour éviter les effets de bord.

### Configuration de l'environnement (1 heure)

#### Partie 1 : Installation de JUnit (30 minutes)

1. **Télécharger et installer IntelliJ IDEA**
   - Téléchargez IntelliJ IDEA depuis le [site officiel](https://www.jetbrains.com/idea/download/).
   - Installez IntelliJ IDEA en suivant les instructions spécifiques à votre système d'exploitation.

2. **Créer un nouveau projet**
   - Ouvrez IntelliJ IDEA.
   - Cliquez sur `File` > `New` > `Project`.
   - Sélectionnez `Java` dans la liste des types de projet.
   - Donnez un nom à votre projet et choisissez un emplacement.
   - Cliquez sur `Finish`.

3. **Ajouter JUnit à votre projet**
   - Cliquez sur `File` > `Project Structure` ou utilisez le raccourci `Ctrl+Alt+Shift+S`.
   - Dans la section `Libraries`, cliquez sur le signe `+` pour ajouter une nouvelle bibliothèque.
   - Sélectionnez `From Maven...`.
   - Dans la boîte de dialogue qui s'affiche, tapez `junit:junit:4.13.2` (ou une version plus récente si disponible).
   - Cliquez sur `OK` et IntelliJ téléchargera et ajoutera JUnit à votre projet.

#### Partie 2 : Configuration de Maven/Gradle pour JUnit (30 minutes)

##### Maven

Ajoutez la dépendance suivante à votre fichier `pom.xml` :

```xml
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.13.2</version>
    <scope>test</scope>
</dependency>
```

##### Gradle

Ajoutez la dépendance suivante à votre fichier `build.gradle` :

```groovy
testImplementation 'junit:junit:4.13.2'
```

### Explication des Annotations des Tests Unitaires

Les annotations dans JUnit sont utilisées pour définir le comportement des méthodes de test et leur cycle de vie. Voici une explication détaillée des principales annotations utilisées dans JUnit :

1. **`@Test`** : Indique que la méthode est une méthode de test. JUnit exécutera cette méthode comme un test lors de l'exécution des tests.

2. **`@BeforeEach`** : Indique qu'une méthode annotée avec `@BeforeEach` doit être exécutée avant chaque méthode de test. Elle est utilisée pour configurer les prérequis nécessaires pour chaque test.

3. **`@AfterEach`** : Indique qu'une méthode annotée avec `@AfterEach` doit être exécutée après chaque méthode de test. Elle est utilisée pour nettoyer les ressources utilisées pendant les tests.

4. **`@BeforeAll`** : Indique qu'une méthode annotée avec `@BeforeAll` doit être exécutée une seule fois avant toutes les méthodes de test dans la classe. Elle est utilisée pour effectuer des configurations globales. La méthode doit être statique.

5. **`@AfterAll`** : Indique qu'une méthode annotée avec `@AfterAll` doit être exécutée une seule fois après toutes les méthodes de test dans la classe. Elle est utilisée pour effectuer des nettoyages globaux. La méthode doit être statique.

### Écriture de Tests Unitaires Simples (3 heures)

#### Partie 1 : Structure d'un test unitaire (1 heure)

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
   import org.junit.jupiter.api.BeforeEach;
   import org.junit.jupiter.api.AfterEach;
   import org.junit.jupiter.api.BeforeAll;
   import org.junit.jupiter.api.AfterAll;
   import org.junit.jupiter.api.Test;

   /**
    * La classe CalculatorTest contient des tests unitaires pour la classe Calculator.
    */
   public class CalculatorTest {
       private Calculator calculator;

       /**
        * Exécuté avant chaque méthode de test. Initialise le calculateur.
        */
       @BeforeEach
       public void setUp() {
           calculator = new Calculator();
       }

       /**
        * Exécuté après chaque méthode de test.
        */
       @AfterEach
       public void tearDown() {
           calculator = null;
       }

       /**
        * Exécuté une fois avant tous les tests. Peut être utilisé pour une configuration globale.
        */
       @BeforeAll
       public static void initAll() {
           System.out.println("Tests démarrés");
       }

       /**
        * Exécuté une fois après tous les tests. Peut être utilisé pour un nettoyage global.
        */
       @AfterAll
       public static void tearDownAll() {
           System.out.println("Tests terminés");
       }

       /**
        * Teste la méthode add pour vérifier que les valeurs sont correctement additionnées.
        */
       @Test
       public void testAdd() {
           assertEquals(5, calculator.add(2, 3), "2 + 3 doit être égal à 5");
           assertEquals(0, calculator.add(0, 0), "0 + 0 doit être égal à 0");
           assertEquals(-5, calculator.add(-2, -3), "-2 + -3 doit être égal à -5");
       }
   }
   ```

#### Partie 2 : Assertions de base (1 heure)

- **assertEquals** : Vérifie que deux valeurs sont égales.
- **assertTrue** : Vérifie qu'une condition est vraie.
- **assertFalse** : Vérifie qu'une condition est fausse.
- **assertNull** : Vérifie qu'un objet est null.
- **assertNotNull** : Vérifie qu'un objet n'est pas null.

1. **Exemple d'utilisation des assertions :**

   ```java
   // Fichier: AssertionTests.java
   import static org.junit.jupiter.api.Assertions.*;
   import org.junit.jupiter.api.Test;

   public class AssertionTests {
       @Test
       public void testAssertions() {
           // Vérifier l'égalité
           assertEquals(5, 5, "Les valeurs doivent être égales");

           // Vérifier que la condition est vraie
           assertTrue(3 > 2, "La condition doit être vraie");

           // Vérifier que la condition est fausse
           assertFalse(3 < 2, "La condition doit être fausse");

           // Vérifier que l'objet est null
           Object obj = null;
           assertNull(obj, "L'objet doit être null");

           // Vérifier que l'objet n'est pas null
           obj = new Object();
           assertNotNull(obj, "L'objet ne doit pas être null");
       }
   }
   ```

#### Partie 3 : Tests de méthodes simples et avec exceptions (1 heure)

1. **Ajouter une méthode avec des exceptions dans la classe `Calculator` :**

   ```java
   // Fichier: Calculator.java
   public class Calculator {
       public int add(int a, int b) {
           return a + b;
       }

       public int divide(int a, int b) {
           if (b == 0) {
               throw new IllegalArgumentException("Division par zéro");
           }
           return a / b;
       }
   }
   ```

2. **Créer des tests pour vérifier les exceptions :**

   ```java
   // Fichier: CalculatorTest.java
   import static org.junit.jupiter.api.Assertions.assertEquals;
   import static org.junit.jupiter.api.Assertions.assertThrows;
   import org.junit.jupiter.api.BeforeEach;
   import org.junit.jupiter.api.AfterEach;
   import org.junit.jupiter.api.BeforeAll;
   import org.junit.jupiter.api.AfterAll;
   import org.junit.jupiter.api.Test;

   public class CalculatorTest {
       private Calculator calculator;

       @BeforeEach
       public void setUp() {
           calculator = new Calculator();
       }

       @AfterEach
       public void tearDown() {
           calculator = null;
       }

       @BeforeAll
       public static void initAll() {
           System.out.println("Tests démarrés");
       }

       @AfterAll
       public static void tearDownAll() {
           System.out.println("Tests terminés");
       }

       @Test
       public void testAdd() {
           assertEquals(5, calculator.add(2, 3), "2 + 3 doit être égal à 5");
           assertEquals(0, calculator.add(0, 0), "0 + 0 doit être égal à 0");
           assertEquals(-5, calculator.add(-2, -3), "-2 + -3 doit être égal à -5");
       }

       @Test
       public void testDivide() {
           assertEquals(2, calculator.divide(4, 2), "4 / 2 doit être égal à 2");
       }

       @Test
       public void testDivideByZero() {
           assertThrows(IllegalArgumentException.class, () -> {
               calculator.divide(4, 0);
           }, "Division par zéro doit lancer une IllegalArgumentException");
       }
   }
```
```
### Pause déjeuner (1 heure)

### Exemples Pratiques (1 heure)

#### Partie 1 : Tests de méthodes simples (30 minutes)

1. **Créer la classe `Person` :**

   ```java
   // Fichier: Person.java
   /**
    * La classe Person représente une personne avec un prénom et un nom de famille.
    */
   public class Person {
       private String firstName;
       private String lastName;

       public Person(String firstName, String lastName) {
           this.firstName = firstName;
           this.lastName = lastName;
       }

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
       @Test
       public void testGetFullName() {
           Person person = new Person("John", "Doe");
           assertEquals("John Doe", person.getFullName(), "Le nom complet doit être 'John Doe'");

           Person person2 = new Person("Jane", "Smith");
           assertEquals("Jane Smith", person2.getFullName(), "Le nom complet doit être 'Jane Smith'");
       }
   }
   ```

#### Partie 2 : Tests de méthodes avec exceptions (30 minutes)

1. **Ajouter des méthodes avec des exceptions dans la classe `BankAccount` :**

   ```java
   // Fichier: BankAccount.java
   /**
    * La classe BankAccount représente un compte bancaire avec des méthodes pour déposer, retirer et transférer des fonds.
    */
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

2. **Créer des tests pour vérifier les exceptions :**

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

### Outils et Pratiques Recommandées (1 heure)

#### Partie 1 : Utilisation de Mocking avec Mockito (30 minutes)

Mockito est un framework de mock permettant de simuler des objets dans vos tests unitaires, ce qui est très utile pour isoler les unités de code et tester leur comportement de manière plus précise.

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

#### Partie 2 : Coverage des Tests avec JaCoCo (30 minutes)

JaCoCo est un outil de couverture de code qui vous aide à voir quelles parties de votre code sont couvertes par des tests et lesquelles ne le sont pas.

1. **Ajouter les dépendances JaCoCo :**

   Ajoutez JaCoCo à votre fichier `pom.xml` (pour Maven) ou `build.gradle` (pour Gradle).

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
           html

.enabled true
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


----

![image](https://github.com/yugmerabtene/DORANCO-2024-CDA-JUnit/assets/3670077/98552ac1-3e97-4088-b9c2-f715c6624541)


### 2. **Cycle de Développement avec Tests (TDD - Test Driven Development)**

#### Qu'est-ce que le TDD ?

Le **Test Driven Development (TDD)**, ou développement dirigé par les tests, est une approche de développement logiciel qui se concentre sur l'écriture de tests avant même de commencer à coder la fonctionnalité réelle. Cette méthode a été popularisée par Kent Beck, l'un des pionniers de l'Extreme Programming (XP). L'objectif principal du TDD est de garantir que le code écrit est toujours testé et que les nouvelles fonctionnalités sont intégrées sans introduire de bugs.

#### Pourquoi utiliser le TDD ?

- **Qualité du Code** : En écrivant les tests en premier, les développeurs sont contraints de penser à la manière dont le code sera utilisé. Cela conduit à un code plus propre et mieux structuré.
- **Réduction des Bugs** : Les tests écrits avant le code aident à identifier et corriger les bugs dès les premières phases du développement.
- **Confiance dans les Refactorisations** : Avec des tests en place, les développeurs peuvent refactoriser le code en toute confiance, sachant que les tests vérifieront que les modifications n'ont pas introduit de nouveaux bugs.
- **Documentation Vivante** : Les tests servent de documentation vivante sur le comportement attendu du code.

![image](https://github.com/yugmerabtene/DORANCO-2024-CDA-JUnit/assets/3670077/86673b93-63f1-4941-ac61-c45594d7509e)


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

---

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



