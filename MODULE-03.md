
### Jour 3: MODULE-03 - Tests de Sécurité

#### Durée: 8 heures

### Objectifs:

1. Comprendre les tests de sécurité
2. Utiliser OWASP ZAP pour tester les vulnérabilités

### Contenu Détaillé:

---

#### Introduction aux Tests de Sécurité (1 heure)

**Partie 1: Importance des tests de sécurité (30 minutes)**
- **Pourquoi les tests de sécurité sont cruciaux :**
  - Protéger les données des utilisateurs.
  - Prévenir les pertes financières.
  - Assurer la conformité avec les réglementations.
  - Maintenir la réputation de l'entreprise.
  
**Partie 2: Types de vulnérabilités courantes (30 minutes)**
- **Vulnérabilités fréquentes :**
  - **XSS (Cross-Site Scripting) :**
    - Injection de scripts malveillants dans des pages web vues par d'autres utilisateurs.
  - **SQL Injection :**
    - Injection de requêtes SQL malveillantes pour accéder ou modifier les bases de données.
  - **CSRF (Cross-Site Request Forgery) :**
    - Forcer un utilisateur authentifié à exécuter des actions indésirables.
  - **Injections Commande :**
    - Injection de commandes système dans des applications vulnérables.

---

#### Introduction à OWASP ZAP (2 heures)

**Partie 1: Installation et configuration (1 heure)**
- **Téléchargement et installation :**
  - Visitez le site officiel de [OWASP ZAP](https://www.zaproxy.org/download/) et téléchargez la version appropriée pour votre OS.
  - Suivez les instructions d'installation spécifiques à votre système (Windows, MacOS, Linux).
  
  ![Installation de OWASP ZAP](https://www.zaproxy.org/img/logo.svg)
  
- **Configuration de base :**
  - **Démarrage de ZAP :**
    - Lancez ZAP et configurez les paramètres initiaux (langue, mode de scan).
  - **Configurer le proxy local :**
    - Paramétrez votre navigateur pour utiliser le proxy de ZAP (généralement localhost:8080).
    - Exemple pour Firefox:
      1. Allez dans `Préférences` > `Paramètres réseau`.
      2. Sélectionnez `Configuration manuelle du proxy`.
      3. Entrez `localhost` et le port `8080` pour le `Proxy HTTP` et `Proxy SSL`.
  - **Importer et configurer des certificats :**
    - Importez les certificats ZAP dans votre navigateur pour intercepter les connexions HTTPS.
      - Pour Firefox, allez dans `Préférences` > `Vie privée & Sécurité` > `Certificats` > `Voir les certificats`.
      - Cliquez sur `Importer` et sélectionnez le certificat de ZAP (généralement disponible dans le répertoire ZAP).

**Partie 2: Interface et fonctionnalités de base (1 heure)**
- **Exploration de l'interface :**
  - **Vue d'ensemble :**
    - **Arborescence des sites :** Liste des sites scannés.
    - **Fenêtre de sortie :** Logs et résultats des scans.
  - **Principales fonctionnalités :**
    - **Quick Start :** Lancer rapidement un scan de base.
    - **Spider :** Explorer automatiquement un site pour trouver des pages et des formulaires.
    - **Active Scan :** Scanner activement pour détecter les vulnérabilités.
    - **HUD (Heads Up Display) :** Interface web intégrée pour faciliter les tests.

---

#### Écriture de Tests de Sécurité (2 heures)

**Partie 1: Scans automatiques (1 heure)**
- **Lancer un scan automatique :**
  - Utilisez l'option Quick Start pour scanner rapidement une URL.
  - Configurer des options avancées (scope, exclusions).

  ```java
  // Exemple de configuration de scan en Java avec OWASP ZAP API
  import org.zaproxy.clientapi.core.ClientApi;
  import org.zaproxy.clientapi.core.ClientApiException;

  public class ZapScanner {
      private static final String ZAP_ADDRESS = "localhost";
      private static final int ZAP_PORT = 8080;
      private static final String ZAP_API_KEY = "changeme";

      public static void main(String[] args) {
          ClientApi api = new ClientApi(ZAP_ADDRESS, ZAP_PORT, ZAP_API_KEY);

          try {
              System.out.println("Starting Spider scan...");
              api.spider.scan("http://example.com");
              // Wait for the spider to complete
              while (true) {
                  Thread.sleep(1000);
                  int progress = Integer.parseInt(api.spider.status("0").toString());
                  System.out.println("Spider progress: " + progress + "%");
                  if (progress >= 100) break;
              }

              System.out.println("Starting Active scan...");
              api.ascan.scan("http://example.com", "True", "False", null, null, null);
              // Wait for the active scan to complete
              while (true) {
                  Thread.sleep(1000);
                  int progress = Integer.parseInt(api.ascan.status("0").toString());
                  System.out.println("Active scan progress: " + progress + "%");
                  if (progress >= 100) break;
              }

              System.out.println("Scan completed.");

          } catch (ClientApiException | InterruptedException e) {
              e.printStackTrace();
          }
      }
  }
  ```

**Partie 2: Tests manuels avec ZAP (1 heure)**
- **Tests manuels :**
  - **Utilisation du HUD :**
    - Intégrez le HUD dans votre session de navigation pour des tests interactifs.
  - **Injection de scripts :**
    - Manuellement injecter des payloads pour tester les vulnérabilités.

---

#### Pause déjeuner (1 heure)

---

#### Exemples Pratiques (2 heures)

**Partie 1: Détection des vulnérabilités XSS (1 heure)**
- **Étapes :**
  - Choisir une cible vulnérable.
  - Utiliser le module de scanner XSS.
  - Analyser et interpréter les résultats.

  ```java
  // Exemple d'injection XSS avec OWASP ZAP API
  import org.zaproxy.clientapi.core.ClientApi;
  import org.zaproxy.clientapi.core.ClientApiException;

  public class ZapXSSScan {
      private static final String ZAP_ADDRESS = "localhost";
      private static final int ZAP_PORT = 8080;
      private static final String ZAP_API_KEY = "changeme";

      public static void main(String[] args) {
          ClientApi api = new ClientApi(ZAP_ADDRESS, ZAP_PORT, ZAP_API_KEY);

          try {
              System.out.println("Starting XSS scan...");
              api.pscan.enableAllScanners();
              api.pscan.scan("http://example.com");

              // Wait for the passive scan to complete
              while (true) {
                  Thread.sleep(1000);
                  int recordsToScan = Integer.parseInt(api.pscan.recordsToScan().toString());
                  if (recordsToScan == 0) break;
              }

              System.out.println("XSS scan completed.");

          } catch (ClientApiException | InterruptedException e) {
              e.printStackTrace();
          }
      }
  }
  ```

**Partie 2: Détection des vulnérabilités SQL Injection (1 heure)**
- **Étapes :**
  - Choisir une cible vulnérable.
  - Utiliser le module de scanner SQLi.
  - Analyser et interpréter les résultats.

  ```java
  // Exemple d'injection SQL avec OWASP ZAP API
  import org.zaproxy.clientapi.core.ClientApi;
  import org.zaproxy.clientapi.core.ClientApiException;

  public class ZapSQLiScan {
      private static final String ZAP_ADDRESS = "localhost";
      private static final int ZAP_PORT = 8080;
      private static final String ZAP_API_KEY = "changeme";

      public static void main(String[] args) {
          ClientApi api = new ClientApi(ZAP_ADDRESS, ZAP_PORT, ZAP_API_KEY);

          try {
              System.out.println("Starting SQL Injection scan...");
              api.pscan.enableAllScanners();
              api.pscan.scan("http://example.com");

              // Wait for the passive scan to complete
              while (true) {
                  Thread.sleep(1000);
                  int recordsToScan = Integer.parseInt(api.pscan.recordsToScan().toString());
                  if (recordsToScan == 0) break;
              }

              System.out.println("SQL Injection scan completed.");

          } catch (ClientApiException | InterruptedException e) {
              e.printStackTrace();
          }
      }
  }
  ```

---

#### Outils et Pratiques Recommandées (1 heure)

**Partie 1: Intégration des tests de sécurité dans le pipeline CI/CD (30 minutes)**
- **Intégration continue :**
  - Utiliser des plugins pour intégrer ZAP dans les pipelines CI/CD (Jenkins, GitLab CI, etc.).
  - Configurer des scans réguliers sur chaque build.

  ```groovy
  // Exemple de pipeline Jenkins avec ZAP
  pipeline {
      agent any
      stages {
          stage('Checkout') {
              steps {
                  checkout scm
              }
          }
          stage('Build') {
              steps {
                  sh './gradlew build'
              }
          }
          stage('ZAP Scan') {
              steps {
                  sh '

zap.sh -daemon -port 8080 -config api.key=changeme'
                  sh 'zap-cli quick-scan http://example.com'
                  sh 'zap-cli report -o zap_report.html -f html'
              }
          }
      }
      post {
          always {
              archiveArtifacts artifacts: 'zap_report.html', allowEmptyArchive: true
          }
      }
  }
  ```

**Partie 2: Utilisation de rapports pour le suivi des vulnérabilités (30 minutes)**
- **Génération de rapports :**
  - Exporter les résultats de scan sous forme de rapports détaillés.
  - Suivi des vulnérabilités avec des outils de gestion (JIRA, Trello).

  ```java
  // Exemple de génération de rapport avec OWASP ZAP API
  import org.zaproxy.clientapi.core.ClientApi;
  import org.zaproxy.clientapi.core.ClientApiException;

  public class ZapReport {
      private static final String ZAP_ADDRESS = "localhost";
      private static final int ZAP_PORT = 8080;
      private static final String ZAP_API_KEY = "changeme";

      public static void main(String[] args) {
          ClientApi api = new ClientApi(ZAP_ADDRESS, ZAP_PORT, ZAP_API_KEY);

          try {
              byte[] report = api.core.htmlreport();
              java.nio.file.Files.write(java.nio.file.Paths.get("zap_report.html"), report);
              System.out.println("Report generated.");

          } catch (ClientApiException | java.io.IOException e) {
              e.printStackTrace();
          }
      }
  }
  ```

---

### Installation et Configuration de OWASP ZAP

1. **Téléchargement et Installation :**
   - Allez sur [la page de téléchargement de OWASP ZAP](https://www.zaproxy.org/download/) et choisissez votre système d'exploitation.
   - Suivez les étapes spécifiques à votre système pour installer ZAP.

2. **Configuration de ZAP :**
   - **Démarrage :** Lancez ZAP et configurez les paramètres initiaux.
   - **Proxy local :**
     - Configurez votre navigateur pour utiliser le proxy de ZAP (par défaut, localhost:8080).
   - **Certificats :**
     - Importez le certificat de ZAP dans votre navigateur pour intercepter les connexions HTTPS.
