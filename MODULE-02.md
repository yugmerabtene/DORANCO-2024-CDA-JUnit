### Jour 2: MODULE-02 - Tests Fonctionnels en Java

#### Durée: 8 heures

---

### Objectifs:

1. Comprendre les tests fonctionnels
2. Utiliser Selenium pour les tests d'interface utilisateur

---

### Contenu:

#### 1. Introduction aux Tests Fonctionnels (1 heure)

**Partie 1: Définition et objectifs (30 minutes)**

**Définition :**
- Les tests fonctionnels visent à vérifier que le système fonctionne conformément aux spécifications.
- Ils se concentrent sur les comportements externes de l'application.

**Objectifs :**
- Valider les fonctionnalités du logiciel.
- Assurer que le système répond aux exigences métier.

**Partie 2: Différences avec les tests unitaires (30 minutes)**

**Tests unitaires :**
- Vérifient des petites parties du code (unités).
- Isolation des composants individuels.

**Tests fonctionnels :**
- Vérifient des scénarios utilisateur complets.
- Interactions entre plusieurs composants.

---

#### 2. Introduction à Selenium (2 heures)

**Partie 1: Configuration de Selenium (1 heure)**

**Installation et Configuration :**

1. **Téléchargez Selenium Java Bindings :**
   - Rendez-vous sur [SeleniumHQ](https://www.selenium.dev/downloads/).
   - Téléchargez le fichier Java.

2. **Téléchargez le WebDriver pour votre navigateur :**
   - Pour Chrome : [ChromeDriver](https://sites.google.com/a/chromium.org/chromedriver/downloads)
   - Pour Firefox : [GeckoDriver](https://github.com/mozilla/geckodriver/releases)

3. **Ajoutez le WebDriver au PATH système :**
   - Décompressez le fichier téléchargé et placez le WebDriver dans un répertoire de votre choix (ex. `C:\WebDrivers` pour Windows ou `/usr/local/bin` pour macOS/Linux).
   - Ajoutez ce répertoire au PATH système.

   **Pour Windows :**
   - Recherchez `Variables d'environnement` dans le menu Démarrer.
   - Cliquez sur `Variables d'environnement`.
   - Dans `Variables système`, sélectionnez `Path` puis cliquez sur `Modifier`.
   - Ajoutez le chemin du répertoire où se trouve votre WebDriver.

   **Pour macOS/Linux :**
   - Ouvrez le terminal et ajoutez la ligne suivante à votre fichier `~/.bash_profile` ou `~/.zshrc` :
     ```sh
     export PATH=$PATH:/path/to/webdriver
     ```
   - Rechargez le profil avec `source ~/.bash_profile` ou `source ~/.zshrc`.

**Setup de WebDriver :**

1. **Ouvrez votre projet Maven dans IntelliJ IDEA**.

2. **Ajoutez les dépendances nécessaires dans `pom.xml` :**

   ```xml
   <dependencies>
       <dependency>
           <groupId>org.seleniumhq.selenium</groupId>
           <artifactId>selenium-java</artifactId>
           <version>4.0.0</version>
       </dependency>
       <dependency>
           <groupId>org.testng</groupId>
           <artifactId>testng</artifactId>
           <version>7.4.0</version>
           <scope>test</scope>
       </dependency>
   </dependencies>
   ```

3. **Synchronisez le projet Maven :**
   - Cliquez sur l'icône `Maven` dans la barre latérale droite.
   - Cliquez sur le bouton `Reload All Maven Projects`.

---

**Partie 2: Structure d'un test Selenium (1 heure)**

**Éléments de base :**

1. **Initialisation de WebDriver :**
   - Ajoutez une classe de test dans `src/test/java`.

   ```java
   import org.openqa.selenium.WebDriver;
   import org.openqa.selenium.chrome.ChromeDriver;
   import org.testng.annotations.AfterClass;
   import org.testng.annotations.BeforeClass;
   import org.testng.annotations.Test;
   import static org.testng.Assert.assertEquals;

   public class BasicTest {
       WebDriver driver;

       @BeforeClass
       public void setup() {
           System.setProperty("webdriver.chrome.driver", "path/to/chromedriver"); // Remplacez par le chemin de votre chromedriver
           driver = new ChromeDriver();
           driver.get("https://www.google.com");
       }

       @Test
       public void testTitle() {
           String title = driver.getTitle();
           assertEquals(title, "Google");
       }

       @AfterClass
       public void teardown() {
           driver.quit();
       }
   }
   ```

2. **Navigation vers une URL :**
   - Dans l'exemple ci-dessus, la ligne `driver.get("https://www.google.com");` navigue vers l'URL spécifiée.

3. **Localisation des éléments :**
   - Utilisez des méthodes comme `findElement(By.name("q"))` pour localiser les éléments de la page.

4. **Effectuer des actions (clics, saisie de texte) :**
   - Utilisez des méthodes comme `click()` et `sendKeys("text")`.

5. **Vérifiez les résultats :**
   - Utilisez des assertions comme `assertEquals()` pour vérifier les résultats.

---

#### 3. Écriture de Tests Fonctionnels (2 heures)

**Partie 1: Interaction avec des éléments web (1 heure)**

**Exemple de code pour interagir avec des éléments sur Google :**

```java
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.annotations.AfterClass;
import org.testng.annotations.BeforeClass;
import org.testng.annotations.Test;

public class GoogleTest {
    WebDriver driver;

    @BeforeClass
    public void setup() {
        System.setProperty("webdriver.chrome.driver", "path/to/chromedriver"); // Remplacez par le chemin de votre chromedriver
        driver = new ChromeDriver();
        driver.get("https://www.google.com");
    }

    @Test
    public void testSearch() {
        // Localiser le champ de recherche
        WebElement searchBox = driver.findElement(By.name("q"));
        searchBox.sendKeys("Selenium WebDriver");

        // Soumettre le formulaire de recherche
        searchBox.submit();

        // Attendre que la page se charge et vérifier le titre
        new WebDriverWait(driver, 10).until(ExpectedConditions.titleContains("Selenium WebDriver"));

        // Vérifier que le titre contient "Selenium WebDriver"
        String title = driver.getTitle();
        Assert.assertTrue(title.contains("Selenium WebDriver"), "Title check failed!");
    }

    @AfterClass
    public void teardown() {
        driver.quit();
    }
}
```

**Partie 2: Assertions et vérifications sur l'interface utilisateur (1 heure)**

**Exemple de code pour les assertions :**

```java
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.Assert;
import org.testng.annotations.AfterClass;
import org.testng.annotations.BeforeClass;
import org.testng.annotations.Test;

public class GoogleAssertionsTest {
    WebDriver driver;

    @BeforeClass
    public void setup() {
        System.setProperty("webdriver.chrome.driver", "path/to/chromedriver");
        driver = new ChromeDriver();
        driver.get("https://www.google.com");
    }

    @Test
    public void testTitle() {
        String title = driver.getTitle();
        Assert.assertEquals(title, "Google");
    }

    @Test
    public void testSearchBoxPresence() {
        WebElement searchBox = driver.findElement(By.name("q"));
        Assert.assertTrue(searchBox.isDisplayed(), "Search box is not displayed!");
    }

    @AfterClass
    public void teardown() {
        driver.quit();
    }
}
```

---

### Pause déjeuner (1 heure)

---

#### 4. Exemples Pratiques (2 heures)

**Partie 1: Tests de formulaires (1 heure)**

**Exemple de test de formulaire de recherche sur Google :**

```java
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.Assert;
import org.testng.annotations.AfterClass;
import org.testng.annotations.BeforeClass;
import org.testng.annotations.Test;

public class GoogleFormTest {
    WebDriver driver;

    @BeforeClass
    public void setup() {
        System.setProperty("webdriver.chrome.driver", "path/to/chromedriver");
        driver = new ChromeDriver();
        driver.get("https://www.google.com");
    }

    @Test
    public void testGoogleSearchForm() {
        WebElement searchBox = driver.findElement(By.name("q"));
        searchBox.sendKeys("TestNG");
        searchBox.submit();

        new WebDriverWait(driver, 10).until(ExpectedConditions.titleContains("TestNG"));

        WebElement resultStats = driver.findElement(By.id("result-stats"));
        Assert.assertTrue(resultStats.isDisplayed(), "Results stats are not displayed!");
    }

    @AfterClass
    public void teardown() {
        driver.quit();
    }
}
```

**Partie 2: Tests de navigation (1 heure)**

**Exemple de test de navigation sur Google :**

```java
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.Assert;
import org.testng.annotations.AfterClass;
import org.testng.annotations.BeforeClass;
import org.testng.annotations.Test;

public class GoogleNavigationTest {
    WebDriver driver;

    @BeforeClass
    public void setup() {
        System.set

Property("webdriver.chrome.driver", "path/to/chromedriver");
        driver = new ChromeDriver();
        driver.get("https://www.google.com");
    }

    @Test
    public void testGoogleAboutNavigation() {
        WebElement aboutLink = driver.findElement(By.linkText("About"));
        aboutLink.click();

        new WebDriverWait(driver, 10).until(ExpectedConditions.titleContains("About Google"));

        String currentUrl = driver.getCurrentUrl();
        Assert.assertTrue(currentUrl.contains("/about/"), "Navigation to About page failed!");
    }

    @AfterClass
    public void teardown() {
        driver.quit();
    }
}
```

---

#### 5. Outils et Pratiques Recommandées (1 heure)

**Partie 1: Utilisation de Page Object Pattern (30 minutes)**

**Exemple de modèle Page Object pour Google :**

```java
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;

public class GoogleSearchPage {
    WebDriver driver;

    By searchBox = By.name("q");

    public GoogleSearchPage(WebDriver driver) {
        this.driver = driver;
    }

    public void setSearchText(String searchText) {
        driver.findElement(searchBox).sendKeys(searchText);
    }

    public void submitSearch() {
        driver.findElement(searchBox).submit();
    }
}

// Utilisation du modèle Page Object
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.Assert;
import org.testng.annotations.AfterClass;
import org.testng.annotations.BeforeClass;
import org.testng.annotations.Test;

public class GoogleSearchTest {
    WebDriver driver;

    @BeforeClass
    public void setup() {
        System.setProperty("webdriver.chrome.driver", "path/to/chromedriver");
        driver = new ChromeDriver();
        driver.get("https://www.google.com");
    }

    @Test
    public void testSearch() {
        GoogleSearchPage searchPage = new GoogleSearchPage(driver);
        searchPage.setSearchText("Selenium WebDriver");
        searchPage.submitSearch();

        new WebDriverWait(driver, 10).until(ExpectedConditions.titleContains("Selenium WebDriver"));

        String title = driver.getTitle();
        Assert.assertTrue(title.contains("Selenium WebDriver"), "Title check failed!");
    }

    @AfterClass
    public void teardown() {
        driver.quit();
    }
}
```

**Partie 2: Exécution des tests dans différents navigateurs avec WebDriver (30 minutes)**

**Exemple d'exécution sur plusieurs navigateurs :**

```java
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.testng.annotations.AfterClass;
import org.testng.annotations.BeforeClass;
import org.testng.annotations.Parameters;
import org.testng.annotations.Test;

public class CrossBrowserTest {
    WebDriver driver;

    @Parameters("browser")
    @BeforeClass
    public void setup(String browser) {
        if(browser.equalsIgnoreCase("chrome")) {
            System.setProperty("webdriver.chrome.driver", "path/to/chromedriver");
            driver = new ChromeDriver();
        } else if(browser.equalsIgnoreCase("firefox")) {
            System.setProperty("webdriver.gecko.driver", "path/to/geckodriver");
            driver = new FirefoxDriver();
        }
        driver.get("https://www.google.com");
    }

    @Test
    public void testTitle() {
        String title = driver.getTitle();
        Assert.assertEquals(title, "Google");
    }

    @AfterClass
    public void teardown() {
        driver.quit();
    }
}
```

---
