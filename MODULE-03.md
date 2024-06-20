### Jour 3: MODULE-03 - Tests de Sécurité

#### Durée: 8 heures

### Objectifs:
1. Comprendre les tests de sécurité
2. Utiliser OWASP ZAP pour tester les vulnérabilités

---

#### Introduction aux Tests de Sécurité (1 heure)

**Partie 1: Importance des tests de sécurité (30 minutes)**
- **Pourquoi les tests de sécurité sont cruciaux :**
  - **Protéger les données des utilisateurs :** Empêcher les violations de données qui pourraient exposer des informations sensibles.
  - **Prévenir les pertes financières :** Réduire les risques de fraudes et d'attaques pouvant entraîner des pertes financières.
  - **Assurer la conformité avec les réglementations :** Respecter les normes de sécurité (GDPR, HIPAA, etc.) pour éviter des amendes et des sanctions.
  - **Maintenir la réputation de l'entreprise :** Préserver la confiance des clients et partenaires en évitant les incidents de sécurité.

**Partie 2: Types de vulnérabilités courantes (30 minutes)**
- **Vulnérabilités fréquentes :**
  - **XSS (Cross-Site Scripting) :**
    - **Description :** Injection de scripts malveillants dans des pages web vues par d'autres utilisateurs.
    - **Impact :** Permet aux attaquants de voler des cookies, usurper des sessions ou défigurer des sites web.
  - **SQL Injection :**
    - **Description :** Injection de requêtes SQL malveillantes pour accéder ou modifier les bases de données.
    - **Impact :** Peut conduire à la divulgation de toutes les informations dans la base de données.
  - **CSRF (Cross-Site Request Forgery) :**
    - **Description :** Forcer un utilisateur authentifié à exécuter des actions indésirables.
    - **Impact :** Peut amener un utilisateur à effectuer des actions non désirées sans son consentement.
  - **Injections Commande :**
    - **Description :** Injection de commandes système dans des applications vulnérables.
    - **Impact :** Peut permettre à un attaquant de prendre le contrôle complet du serveur.

---

#### Installation et Configuration de OWASP ZAP (1 heure)

**Partie 1: Téléchargement et installation (30 minutes)**
- **Téléchargement et installation :**
  - Visitez le site officiel de [OWASP ZAP](https://www.zaproxy.org/download/) et téléchargez la version appropriée pour votre OS.
  - Suivez les instructions d'installation spécifiques à votre système :
    - **Windows :** Exécutez l'installeur téléchargé et suivez les instructions à l'écran.
    - **MacOS :** Montez l'image disque téléchargée et déplacez OWASP ZAP dans le dossier Applications.
    - **Linux :** Extrayez l'archive téléchargée et lancez le script `zap.sh`.

  ![Installation de OWASP ZAP](https://www.zaproxy.org/img/logo.svg)

**Partie 2: Configuration de base (30 minutes)**
  - **Démarrage de ZAP :**
    - Lancez ZAP et configurez les paramètres initiaux :
      - **Langue :** Choisissez votre langue préférée.
      - **Mode de scan :** Sélectionnez le mode adapté à votre niveau (débutant, intermédiaire, avancé).
  - **Configurer le proxy local :**
    - **Pour Firefox :**
      1. Allez dans `Préférences` > `Paramètres réseau`.
      2. Sélectionnez `Configuration manuelle du proxy`.
      3. Entrez `localhost` et le port `8080` pour le `Proxy HTTP` et `Proxy SSL`.
      4. Cliquez sur `OK` pour enregistrer les modifications.
  - **Importer et configurer des certificats :**
    - **Pour Firefox :**
      1. Allez dans `Préférences` > `Vie privée & Sécurité` > `Certificats` > `Voir les certificats`.
      2. Cliquez sur `Importer` et sélectionnez le certificat de ZAP (généralement disponible dans le répertoire ZAP).
      3. Suivez les instructions pour importer le certificat et redémarrez le navigateur si nécessaire.

---

#### Exploration de l'Interface et Fonctionnalités de Base (1 heure)

**Partie 1: Exploration de l'interface (30 minutes)**
  - **Vue d'ensemble :**
    - **Arborescence des sites :** Liste des sites scannés.
    - **Fenêtre de sortie :** Logs et résultats des scans.
    - **Panneau de contrôle :** Accès rapide aux principales fonctionnalités et configurations.
  - **Comprendre les différentes sections :**
    - **Sites :** Affiche la structure du site scanné.
    - **Alertes :** Liste des vulnérabilités détectées.
    - **Historique :** Enregistre toutes les requêtes et réponses HTTP.

**Partie 2: Principales fonctionnalités (30 minutes)**
  - **Quick Start :** Lancer rapidement un scan de base.
    - Cliquez sur `Quick Start` puis entrez l'URL de la cible et cliquez sur `Attack`.
  - **Spider :** Explorer automatiquement un site pour trouver des pages et des formulaires.
    - Sélectionnez une URL dans l'arborescence des sites, cliquez droit et choisissez `Attack` > `Spider`.
  - **Active Scan :** Scanner activement pour détecter les vulnérabilités.
    - Sélectionnez une URL dans l'arborescence des sites, cliquez droit et choisissez `Attack` > `Active Scan`.
  - **HUD (Heads Up Display) :** Interface web intégrée pour faciliter les tests.
    - Activez le HUD depuis le panneau de configuration et naviguez sur le site cible pour voir les indicateurs de vulnérabilités en temps réel.

---

#### Écriture de Tests de Sécurité (2 heures)

**Partie 1: Scans automatiques (1 heure)**
- **Lancer un scan automatique :**
  - Utilisez l'option Quick Start pour scanner rapidement une URL.
  - Configurer des options avancées :
    - **Scope :** Définir la portée du scan pour inclure/exclure certaines parties du site.
    - **Exclusions :** Spécifier les URL ou motifs à exclure du scan.

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
    - **Avantages du HUD :**
      - Visualisation des vulnérabilités en temps réel.
      - Interface conviviale pour exécuter des attaques manuelles.
  - **Injection de scripts :**
    - Manuellement injecter des payloads pour tester les vulnérabilités.
    - **Exemple de test XSS :**
      - Naviguez jusqu'à un formulaire d'entrée.
      - Saisissez un payload XSS comme `<script>alert('XSS')</script>` dans un champ de texte.
      - Soumettez le formulaire et observez si l'alerte JavaScript est exécutée.

---

#### Pause déjeuner (1 heure)

---

#### Exemples Pratiques (2 heures)

**Partie 1: Détection des vulnérabilités XSS (1 heure)**
- **Étapes :**
  - Choisir une cible vulnérable.
  - Utiliser le module de scanner XSS.
  - Analyser et interpréter les résultats.
    - **Vérification des alertes :** Consulter les alertes générées par ZAP pour les entrées XSS.
    - **Examen des requêtes/réponses :** Analyser les requêtes HTTP et les réponses pour identifier les vulnérabilités exploité

es.

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
    - **Vérification des alertes :** Consulter les alertes générées par ZAP pour les injections SQL.
    - **Examen des requêtes/réponses :** Analyser les requêtes HTTP et les réponses pour identifier les vulnérabilités exploitées.

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

#### Intégration des Tests de Sécurité dans le Pipeline CI/CD (2 heures)

**Partie 1: Présentation et configuration (30 minutes)**
- **Intégration continue :**
  - **Présentation :** Comprendre l'importance d'intégrer les tests de sécurité dans le pipeline CI/CD.
  - **Configuration de base :** Utilisation de GitHub Actions pour automatiser les scans de sécurité avec OWASP ZAP.

**Partie 2: Configuration de GitHub Actions (1 heure 30 minutes)**
- **Étapes détaillées :**
  1. **Créer un fichier de workflow GitHub Actions :**
     - Créez un répertoire `.github/workflows` à la racine de votre projet.
     - Ajoutez un fichier `zap_scan.yml` dans ce répertoire.

  ```yaml
  name: OWASP ZAP Scan

  on:
    push:
      branches:
        - main
    pull_request:
      branches:
        - main

  jobs:
    zap_scan:
      runs-on: ubuntu-latest

      steps:
      - name: Checkout repository
        uses: actions/checkout@v2

      - name: Start OWASP ZAP
        run: |
          docker run -d --name zap -p 8080:8080 -i owasp/zap2docker-stable zap.sh -daemon -port 8080 -host 0.0.0.0

      - name: Run ZAP baseline scan
        run: |
          docker exec zap zap-baseline.py -t http://example.com -r zap_report.html

      - name: Upload ZAP report
        uses: actions/upload-artifact@v2
        with:
          name: ZAP Report
          path: zap_report.html
  ```

  2. **Explication du fichier de workflow :**
     - **Déclencheurs :** Le workflow s'exécute sur chaque push ou pull request vers la branche principale.
     - **Jobs :** Le job `zap_scan` s'exécute sur un environnement `ubuntu-latest`.
     - **Étapes :**
       - **Checkout du dépôt :** Utilise l'action `actions/checkout@v2` pour extraire le code du dépôt.
       - **Démarrer OWASP ZAP :** Utilise Docker pour lancer OWASP ZAP en mode démon.
       - **Exécuter le scan de base ZAP :** Exécute le scan de base de ZAP sur l'URL spécifiée et génère un rapport HTML.
       - **Télécharger le rapport ZAP :** Utilise l'action `actions/upload-artifact@v2` pour enregistrer le rapport généré.

  3. **Configurer les secrets GitHub :**
     - Si nécessaire, ajoutez des secrets pour l'API de ZAP ou d'autres configurations sensibles dans les paramètres du dépôt GitHub.
       - Allez dans `Settings` > `Secrets` > `New repository secret`.
       - Ajoutez les clés nécessaires comme `ZAP_API_KEY`.

  4. **Exécuter et vérifier les résultats :**
     - Poussez les modifications vers le dépôt GitHub.
     - Vérifiez les exécutions du workflow dans l'onglet "Actions" du dépôt.
     - Téléchargez et analysez le rapport ZAP pour identifier les vulnérabilités.
     - **Interprétation du rapport :**
       - **Alertes :** Chaque alerte identifie une vulnérabilité potentielle.
       - **Description :** Les détails de la vulnérabilité détectée.
       - **Recommandations :** Actions suggérées pour remédier à la vulnérabilité.

---

#### Outils et Pratiques Recommandées (1 heure)

**Partie 1: Utilisation de rapports pour le suivi des vulnérabilités (30 minutes)**
- **Génération de rapports :**
  - Exporter les résultats de scan sous forme de rapports détaillés.
  - Utiliser OWASP ZAP pour générer des rapports en divers formats (HTML, XML, JSON).

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

**Partie 2: Suivi des vulnérabilités avec des outils de gestion (30 minutes)**
- **Intégration avec des outils de gestion de projets :**
  - Utiliser des outils comme JIRA ou Trello pour suivre les vulnérabilités détectées.
  - **JIRA :**
    - Créez des tickets pour chaque vulnérabilité détectée.
    - Assignez les tickets aux membres de l'équipe pour résolution.
    - Utilisez des workflows personnalisés pour suivre la progression des corrections.
  - **Trello :**
    - Créez des cartes pour chaque vulnérabilité.
    - Utilisez des listes pour organiser les vulnérabilités par statut (à faire, en cours, terminé).
    - Assignez les cartes aux membres de l'équipe et suivez les commentaires et les mises à jour.

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

---


érabilités courantes comme XSS et SQL Injection, et des stratégies pour le suivi des vulnérabilités détectées.
