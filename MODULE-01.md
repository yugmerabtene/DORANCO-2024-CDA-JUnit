### Module-01 : Tests unitaires avec jUnit

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

### Classe `User`
La classe `User` représente un utilisateur avec un prénom et un nom de famille.

```java
package fr.doranco;

public class User {
    private String firstName;
    private String lastName;

    public User(String firstName, String lastName) {
        this.firstName = firstName;
        this.lastName = lastName;
    }

    public String getFullName() {
        return firstName + " " + lastName;
    }
}
```

### Interface `UserRepository`
L'interface `UserRepository` définit une méthode pour trouver un utilisateur par son identifiant.

```java
package fr.doranco;

public interface UserRepository {
    User findById(int id);
}
```

### Classe `UserService`
La classe `UserService` utilise un `UserRepository` pour obtenir des utilisateurs.

```java
package fr.doranco;

public class UserService {
    private UserRepository userRepository;

    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public User getUserById(int id) {
        return userRepository.findById(id);
    }
}
```

### Classe de Test `UserServiceTest`
Cette classe contient le test pour la méthode `getUserById` de `UserService`.

```java
package fr.doranco;

import static org.mockito.Mockito.*;
import static org.junit.jupiter.api.Assertions.*;
import org.junit.jupiter.api.Test;

public class UserServiceTest {
    @Test
    public void testGetUserById() {
        // Crée un mock de UserRepository
        UserRepository mockRepo = mock(UserRepository.class);
        
        // Crée une instance de UserService avec le mock UserRepository
        UserService userService = new UserService(mockRepo);

        // Crée un utilisateur factice
        User mockUser = new User("John", "Doe");
        
        // Définit le comportement du mock : lorsque findById(1) est appelé, retourne mockUser
        when(mockRepo.findById(1)).thenReturn(mockUser);

        // Appelle la méthode getUserById et vérifie le résultat
        User result = userService.getUserById(1);
        assertEquals("John Doe", result.getFullName());
    }
}
```

### Explication en Détail du Test

1. **Création du Mock de `UserRepository` :**
   ```java
   UserRepository mockRepo = mock(UserRepository.class);
   ```
   On utilise `Mockito` pour créer un mock de l'interface `UserRepository`. Un mock est un objet simulé qui imite le comportement de vraies instances dans des conditions contrôlées.

2. **Création de l'Instance de `UserService` :**
   ```java
   UserService userService = new UserService(mockRepo);
   ```
   On passe le mock de `UserRepository` au constructeur de `UserService`. Cela permet à `UserService` d'utiliser le mock au lieu d'une implémentation réelle de `UserRepository`.

3. **Création d'un Utilisateur Factice :**
   ```java
   User mockUser = new User("John", "Doe");
   ```
   On crée un objet `User` factice pour simuler un utilisateur avec les prénoms et noms "John Doe".

4. **Définition du Comportement du Mock :**
   ```java
   when(mockRepo.findById(1)).thenReturn(mockUser);
   ```
   On utilise `Mockito` pour spécifier que lorsque la méthode `findById(1)` est appelée sur le mock `UserRepository`, elle doit retourner l'utilisateur factice `mockUser`.

5. **Appel de la Méthode et Vérification du Résultat :**
   ```java
   User result = userService.getUserById(1);
   assertEquals("John Doe", result.getFullName());
   ```
   On appelle la méthode `getUserById(1)` de `UserService` et on vérifie que le nom complet de l'utilisateur retourné est bien "John Doe".

### Utilité de Mockito
`Mockito` est une bibliothèque de simulation pour Java utilisée pour créer des objets factices (mocks) dans les tests unitaires. Son utilité principale est de :

1. **Isoler le Code à Tester :** En utilisant des mocks, on peut isoler la classe à tester (ici, `UserService`) de ses dépendances externes (`UserRepository`), ce qui permet de tester son comportement de manière indépendante.

2. **Contrôler les Scénarios de Test :** Les mocks permettent de définir des comportements spécifiques pour les dépendances, facilitant la simulation de divers scénarios (comme le retour d'un utilisateur spécifique pour un identifiant donné).

3. **Faciliter les Tests :** Les mocks rendent les tests plus rapides et plus simples car ils ne nécessitent pas de configuration de bases de données ou d'autres ressources externes.

Ce test utilise Mockito pour vérifier que la méthode `getUserById` de `UserService` fonctionne correctement en renvoyant le bon utilisateur lorsqu'elle est appelée avec un identifiant donné.

Voici une version corrigée et complète de la procédure pour configurer et utiliser JaCoCo avec Maven, avec des explications détaillées pour chaque étape :

### Partie 2 : Coverage des Tests avec JaCoCo (30 minutes)

JaCoCo est un outil de couverture de code qui vous aide à voir quelles parties de votre code sont couvertes par des tests et lesquelles ne le sont pas.

### Étapes pour Configurer JaCoCo avec Maven

#### 1. Ajouter les Dépendances JaCoCo

Ajoutez JaCoCo à votre fichier `pom.xml`.

**Fichier `pom.xml` Complet avec JaCoCo**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>fr.doranco</groupId>
    <artifactId>testUnitaire</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

    <dependencies>
        <!-- Dépendance pour JUnit Jupiter API -->
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-api</artifactId>
            <version>5.8.2</version>
            <scope>test</scope>
        </dependency>

        <!-- Dépendance pour JUnit Jupiter Engine -->
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-engine</artifactId>
            <version>5.8.2</version>
            <scope>test</scope>
        </dependency>

        <!-- Dépendance pour Mockito -->
        <dependency>
            <groupId>org.mockito</groupId>
            <artifactId>mockito-core</artifactId>
            <version>3.1.0</version>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <!-- Plugin JaCoCo pour la couverture de code -->
            <plugin>
                <groupId>org.jacoco</groupId>
                <artifactId>jacoco-maven-plugin</artifactId>
                <version>0.8.7</version>
                <executions>
                    <!-- Prépare l'agent JaCoCo avant l'exécution des tests -->
                    <execution>
                        <goals>
                            <goal>prepare-agent</goal>
                        </goals>
                    </execution>
                    <!-- Génère le rapport de couverture après l'exécution des tests -->
                    <execution>
                        <id>report</id>
                        <phase>test</phase>
                        <goals>
                            <goal>report</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
</project>
```

#### 2. Analyser la Couverture des Tests

Exécutez vos tests et générez le rapport de couverture avec les commandes Maven suivantes.

**Avec Maven :**

```bash
mvn clean test
mvn jacoco:report
```

- **mvn clean test**: Cette commande nettoie le projet, compile le code source, et exécute les tests définis dans le projet. JaCoCo est configuré pour surveiller l'exécution des tests et enregistrer les informations de couverture de code.
- **mvn jacoco:report**: Cette commande génère un rapport HTML détaillant la couverture de code pour les tests exécutés.

#### 3. Visualiser les Résultats

Ouvrez le fichier `target/site/jacoco/index.html` pour voir le rapport de couverture. Vous y verrez les classes et méthodes couvertes et non couvertes par vos tests.

### Explications Détailées

1. **Configuration du Plugin JaCoCo** :
   - Le plugin JaCoCo est ajouté sous la section `<plugins>` dans le `pom.xml`.
   - **`prepare-agent`**: Configure l'agent JaCoCo pour surveiller la couverture de code pendant l'exécution des tests.
   - **`report`**: Génère un rapport de couverture de code après l'exécution des tests.

2. **Exécution des Tests** :
   - La commande `mvn clean test` nettoie le projet, compile le code source et exécute les tests.
   - Pendant l'exécution des tests, l'agent JaCoCo surveille quelles parties du code sont exécutées.

3. **Génération du Rapport de Couverture** :
   - La commande `mvn jacoco:report` génère un rapport de couverture basé sur les données collectées par l'agent JaCoCo.
   - Le rapport est généré dans le dossier `target/site/jacoco/` sous forme de fichier HTML.

4. **Visualisation du Rapport** :
   - Ouvrez le fichier `index.html` dans le répertoire `target/site/jacoco/`.
   - Le rapport montre le pourcentage de lignes et de branches de votre code couvertes par les tests, ainsi que des détails sur les classes et méthodes spécifiques.

### Résumé des Commandes Maven Utilisées

- **`mvn clean`**: Nettoie le projet en supprimant le répertoire `target`.
- **`mvn test`**: Compile le code et exécute les tests.
- **`mvn jacoco:report`**: Génère un rapport de couverture de code basé sur l'exécution des tests.


Si cela ne marche toujours pas installer la varibale d'environnement : 

## Configuration sur Windows

### Configuration de `JAVA_HOME`

1. **Télécharger et installer le JDK:**
   - Téléchargez le JDK depuis le site officiel d'Oracle : [Java SE Downloads](https://www.oracle.com/java/technologies/javase-downloads.html).
   - Installez le JDK. Notez le chemin d'installation, par exemple `C:\Program Files\Java\jdk-17`.

2. **Configurer `JAVA_HOME`:**
   - Ouvrez le Panneau de configuration.
   - Allez dans **Système et sécurité** > **Système**.
   - Cliquez sur **Paramètres système avancés**.
   - Dans la fenêtre Propriétés système, cliquez sur **Variables d'environnement**.
   - Cliquez sur **Nouvelle...** sous les variables système.
   - Ajoutez une nouvelle variable appelée `JAVA_HOME` et réglez-la sur le chemin d'installation du JDK, par exemple `C:\Program Files\Java\jdk-17`.
   - Cliquez sur **OK** pour fermer les fenêtres.

3. **Modifier la variable `Path`:**
   - Dans les variables système, trouvez et sélectionnez la variable `Path`, puis cliquez sur **Modifier...**.
   - Ajoutez `%JAVA_HOME%\bin` à la liste des chemins.
   - Cliquez sur **OK** pour fermer les fenêtres.

4. **Vérifier la configuration:**
   - Ouvrez une nouvelle fenêtre de commande (cmd) et tapez :
     ```bash
     echo %JAVA_HOME%
     ```
   - Cela devrait afficher le chemin vers le répertoire JDK.
   - Ensuite, tapez :
     ```bash
     java -version
     ```
   - Vous devriez voir la version de Java installée.

### Configuration de `MAVEN_HOME`

1. **Télécharger Maven:**
   - Allez sur le site officiel de Maven : [Apache Maven Download](https://maven.apache.org/download.cgi).
   - Téléchargez la version binaire (zip) de Maven.

2. **Extraire Maven:**
   - Extrayez le fichier zip téléchargé dans un répertoire de votre choix, par exemple `C:\Program Files\Apache\maven`.

3. **Configurer `MAVEN_HOME` et `M2_HOME`:**
   - Ouvrez le Panneau de configuration.
   - Allez dans **Système et sécurité** > **Système**.
   - Cliquez sur **Paramètres système avancés**.
   - Dans la fenêtre Propriétés système, cliquez sur **Variables d'environnement**.
   - Cliquez sur **Nouvelle...** sous les variables système.
   - Ajoutez une nouvelle variable appelée `MAVEN_HOME` et réglez-la sur le chemin où vous avez extrait Maven, par exemple `C:\Program Files\Apache\maven`.
   - Ajoutez une autre variable appelée `M2_HOME` et réglez-la sur le même chemin.
   - Cliquez sur **OK** pour fermer les fenêtres.

4. **Modifier la variable `Path`:**
   - Dans les variables système, trouvez et sélectionnez la variable `Path`, puis cliquez sur **Modifier...**.
   - Ajoutez `%MAVEN_HOME%\bin` à la liste des chemins.
   - Cliquez sur **OK** pour fermer les fenêtres.

5. **Vérifier l'installation:**
   - Ouvrez une nouvelle fenêtre de commande (cmd) et tapez :
     ```bash
     mvn -version
     ```
   - Si Maven est correctement configuré, vous devriez voir la version de Maven et d'autres détails s'afficher.

## Configuration sur Linux/MacOS

### Configuration de `JAVA_HOME`

1. **Télécharger et installer le JDK:**
   - Téléchargez le JDK depuis le site officiel d'Oracle : [Java SE Downloads](https://www.oracle.com/java/technologies/javase-downloads.html).
   - Installez le JDK. Notez le chemin d'installation, par exemple `/usr/lib/jvm/java-17-openjdk`.

2. **Configurer `JAVA_HOME`:**
   - Ouvrez le fichier `~/.bashrc` ou `~/.zshrc` dans un éditeur de texte et ajoutez les lignes suivantes :
     ```bash
     export JAVA_HOME=/usr/lib/jvm/java-17-openjdk
     export PATH=$JAVA_HOME/bin:$PATH
     ```
   - Remplacez `/usr/lib/jvm/java-17-openjdk` par le chemin correct vers votre installation JDK.

3. **Appliquer les changements:**
   - Rechargez le fichier de configuration :
     ```bash
     source ~/.bashrc
     ```
     ou
     ```bash
     source ~/.zshrc
     ```

4. **Vérifier la configuration:**
   - Ouvrez un nouveau terminal et tapez :
     ```bash
     echo $JAVA_HOME
     ```
   - Cela devrait afficher le chemin vers le répertoire JDK.
   - Ensuite, tapez :
     ```bash
     java -version
     ```
   - Vous devriez voir la version de Java installée.

### Configuration de `MAVEN_HOME`

1. **Télécharger Maven:**
   - Allez sur le site officiel de Maven : [Apache Maven Download](https://maven.apache.org/download.cgi).
   - Téléchargez la version binaire (tar.gz) de Maven.

2. **Extraire Maven:**
   - Ouvrez un terminal et extrayez le fichier téléchargé :
     ```bash
     tar xzvf apache-maven-<version>-bin.tar.gz
     ```

3. **Configurer `MAVEN_HOME`:**
   - Ouvrez le fichier `~/.bashrc` ou `~/.zshrc` dans un éditeur de texte et ajoutez les lignes suivantes :
     ```bash
     export MAVEN_HOME=/path/to/apache-maven-<version>
     export PATH=$MAVEN_HOME/bin:$PATH
     ```
   - Remplacez `/path/to/apache-maven-<version>` par le chemin où vous avez extrait Maven.

4. **Appliquer les changements:**
   - Rechargez le fichier de configuration :
     ```bash
     source ~/.bashrc
     ```
     ou
     ```bash
     source ~/.zshrc
     ```

5. **Vérifier l'installation:**
   - Ouvrez un nouveau terminal et tapez :
     ```bash
     mvn -version
     ```
   - Si Maven est correctement configuré, vous devriez voir la version de Maven et d'autres détails s'afficher.





### Configuration de JaCoCo dans le fichier `pom.xml`

#### Voici la configuration complète du fichier `pom.xml` avec JaCoCo :

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>fr.doranco</groupId>
    <artifactId>testUnitaire</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

    <dependencies>
        <!-- Dépendance pour JUnit Jupiter API -->
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-api</artifactId>
            <version>5.8.2</version>
            <scope>test</scope>
        </dependency>

        <!-- Dépendance pour JUnit Jupiter Engine -->
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-engine</artifactId>
            <version>5.8.2</version>
            <scope>test</scope>
        </dependency>

        <!-- Dépendance pour Mockito -->
        <dependency>
            <groupId>org.mockito</groupId>
            <artifactId>mockito-core</artifactId>
            <version>3.1.0</version>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <!-- Plugin JaCoCo pour la couverture de code -->
            <plugin>
                <groupId>org.jacoco</groupId>
                <artifactId>jacoco-maven-plugin</artifactId>
                <version>0.8.7</version>
                <executions>
                    <!-- Prépare l'agent JaCoCo avant l'exécution des tests -->
                    <execution>
                        <goals>
                            <goal>prepare-agent</goal>
                        </goals>
                    </execution>
                    <!-- Génère le rapport de couverture après l'exécution des tests -->
                    <execution>
                        <id>report</id>
                        <phase>test</phase>
                        <goals>
                            <goal>report</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
</project>
```

### Exécution des Tests et Génération du Rapport de Couverture

1. **Nettoyer le projet et exécuter les tests** :
   ```sh
   mvn clean test
   ```

2. **Générer le rapport JaCoCo** :
   ```sh
   mvn jacoco:report
   ```

### Visualiser les Résultats

Ouvrez le fichier `target/site/jacoco/index.html` pour voir le rapport de couverture. Vous y verrez les classes et méthodes couvertes et non couvertes par vos tests.

### Résumé des Étapes

1. **Installer Maven** : Téléchargez et installez Maven, puis configurez la variable d'environnement `PATH`.
2. **Vérifier l'installation** : Utilisez la commande `mvn -v` pour vérifier que Maven est correctement installé.
3. **Configurer JaCoCo** : Ajoutez le plugin JaCoCo à votre fichier `pom.xml`.
4. **Exécuter les commandes Maven** : Utilisez les commandes `mvn clean test` et `mvn jacoco:report` pour exécuter les tests et générer le rapport de couverture.
5. **Visualiser le rapport** : Ouvrez le fichier `target/site/jacoco/index.html` pour voir les résultats de la couverture des tests.



### Ce qu'il faut retenir

avec la méthodologie TDD, nous avons d'abord écrit des tests qui échouent pour chaque fonctionnalité requise. Ensuite, nous avons implémenté le code pour faire passer ces tests. Enfin, nous avons refactorisé le code pour améliorer sa lisibilité et sa maintenance. Cette approche garantit que notre code est testé et fonctionne comme prévu, tout en étant propre et bien structuré.
