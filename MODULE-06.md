### Présentation de Docker

#### Qu'est-ce que Docker ?

Docker est une plateforme logicielle qui permet de créer, déployer et exécuter des applications facilement grâce à la technologie des conteneurs. Les conteneurs encapsulent une application avec toutes ses dépendances, bibliothèques et configurations nécessaires pour fonctionner, garantissant ainsi que l'application s'exécute de manière identique quel que soit l'environnement.

#### Historique

Docker a été lancé en 2013 par la société Docker, Inc. Depuis, il est devenu un standard de facto pour le développement et le déploiement de logiciels en conteneurs. Il a considérablement influencé l'industrie informatique en simplifiant le processus de gestion des environnements applicatifs.

#### Principales Composantes de Docker

1. **Docker Engine** : Le moteur Docker est le cœur de la plateforme, permettant la construction et l'exécution des conteneurs. Il se compose du serveur Docker (daemon), de l'API REST et du client CLI Docker.

2. **Images Docker** : Une image Docker est un modèle en lecture seule utilisé pour créer des conteneurs. Une image contient tout ce dont une application a besoin pour fonctionner : code, runtime, bibliothèques, variables d'environnement et fichiers de configuration.

3. **Conteneurs Docker** : Les conteneurs sont des instances en cours d'exécution d'images Docker. Ils sont légers, portables et isolés, offrant une alternative plus efficace que les machines virtuelles traditionnelles.

4. **Docker Hub** : Docker Hub est un registre public où les développeurs peuvent stocker et partager des images Docker. Il permet également de trouver des images pré-construites pour divers logiciels et services.

5. **Docker Compose** : Un outil permettant de définir et de gérer des applications multi-conteneurs. Avec Docker Compose, vous pouvez utiliser un fichier YAML pour configurer les services de votre application.

#### Avantages de Docker

- **Portabilité** : Les conteneurs peuvent être exécutés de manière cohérente sur n'importe quel environnement qui supporte Docker.
- **Isolation** : Chaque conteneur fonctionne de manière isolée, ce qui réduit les conflits entre les dépendances des applications.
- **Efficacité** : Les conteneurs partagent le noyau du système hôte, ce qui les rend plus légers et plus rapides à démarrer que les machines virtuelles.
- **Scalabilité** : Docker facilite le déploiement et la gestion d'applications distribuées et microservices, permettant une mise à l'échelle simple et efficace.

#### Cas d'Utilisation

- **Développement et Test** : Les développeurs utilisent Docker pour créer des environnements de développement consistants et isolés.
- **Déploiement en Production** : Docker simplifie le déploiement des applications en fournissant un environnement cohérent entre le développement, les tests et la production.
- **Microservices** : Docker est idéal pour la mise en œuvre de l'architecture microservices, où chaque service est isolé et peut être déployé indépendamment.
- **CI/CD** : Docker est souvent utilisé dans les pipelines d'intégration et de déploiement continu pour garantir que les applications sont testées et déployées dans un environnement propre et reproductible.

Pour plus d'informations, vous pouvez consulter la documentation officielle de Docker : [Docker Documentation](https://docs.docker.com/).


![Sans titre](https://github.com/yugmerabtene/DORANCO-2024-CDA-JUnit/assets/3670077/85d50457-0f60-4548-9037-7fc768638e6d)



### Installation de Docker sur votre PC

1. **Télécharger Docker Desktop** :
   - Allez sur le site officiel de Docker : [Docker Desktop](https://www.docker.com/products/docker-desktop) et téléchargez la version correspondant à votre système d'exploitation (Windows, macOS ou Linux).

2. **Installer Docker Desktop** :
   - Suivez les instructions d'installation pour votre système d'exploitation :
     - **Windows** : Exécutez le fichier .exe téléchargé et suivez les instructions de l'assistant d'installation. Vous devrez peut-être redémarrer votre ordinateur après l'installation.
     - **macOS** : Ouvrez le fichier .dmg téléchargé et déplacez Docker dans le dossier Applications. Lancez Docker depuis le dossier Applications.
     - **Linux** : Suivez les instructions spécifiques à votre distribution sur le site officiel de Docker.

3. **Vérifier l'installation** :
   - Ouvrez une fenêtre de terminal ou de commande et exécutez :
     ```bash
     docker --version
     ```
   - Vous devriez voir la version de Docker installée.

4. **Installer Docker Compose** (si ce n'est pas inclus avec Docker Desktop) :
   - Vous pouvez vérifier si Docker Compose est déjà installé en exécutant :
     ```bash
     docker-compose --version
     ```
   - Si Docker Compose n'est pas installé, suivez les instructions sur le site officiel : [Docker Compose Install](https://docs.docker.com/compose/install/).

### Configuration de l'environnement de développement avec Docker

1. **Créer un dossier de projet** :
   - Créez un nouveau dossier pour votre projet, par exemple `my-php-app`.

2. **Créer la structure de dossiers** :
   - À l'intérieur de votre projet, créez les dossiers suivants :
     ```bash
     my-php-app/
     ├── src/
     ├── docker-compose.yml
     ├── Dockerfile
     ├── .dockerignore
     ```

### Étape 1 : Configuration des fichiers Docker

1. **Créer le Dockerfile** :
   - À la racine de votre projet, créez un fichier nommé `Dockerfile` avec le contenu suivant :
     ```dockerfile
     # Utiliser une image de base officielle PHP avec Apache
     FROM php:7.4-apache

     # Installer les extensions nécessaires pour MySQL
     RUN docker-php-ext-install mysqli pdo pdo_mysql

     # Copier les fichiers de l'application dans le répertoire de travail de l'image
     COPY src/ /var/www/html/

     # Donner les permissions correctes au répertoire de travail
     RUN chown -R www-data:www-data /var/www/html
     ```

2. **Créer le fichier docker-compose.yml** :
   - À la racine de votre projet, créez un fichier nommé `docker-compose.yml` avec le contenu suivant :
     ```yaml
     version: '3.1'

     services:
       web:
         build: .
         ports:
           - "8080:80"
         volumes:
           - ./src:/var/www/html
         depends_on:
           - db

       db:
         image: mysql:5.7
         restart: always
         environment:
           MYSQL_ROOT_PASSWORD: root
           MYSQL_DATABASE: testdb
           MYSQL_USER: user
           MYSQL_PASSWORD: password
         ports:
           - "3306:3306"
         volumes:
           - db_data:/var/lib/mysql

     volumes:
       db_data:
     ```

3. **Créer le fichier .dockerignore** :
   - À la racine de votre projet, créez un fichier nommé `.dockerignore` avec le contenu suivant :
     ```
     .git
     node_modules
     vendor
     ```

### Étape 2 : Code de l'application

1. **Créer les fichiers de l'application** :
   - Créez les fichiers suivants dans le dossier `src` :

   **index.php** :
   ```php
   <?php
   $mysqli = new mysqli("db", "user", "password", "testdb");

   if ($mysqli->connect_error) {
       die("Connection failed: " . $mysqli->connect_error);
   }

   $result = $mysqli->query("SELECT * FROM users");
   ?>

   <!DOCTYPE html>
   <html>
   <head>
       <title>CRUD App</title>
       <link rel="stylesheet" href="style.css">
   </head>
   <body>
       <h1>Users</h1>
       <table>
           <tr>
               <th>ID</th>
               <th>Name</th>
               <th>Email</th>
               <th>Actions</th>
           </tr>
           <?php while($row = $result->fetch_assoc()): ?>
           <tr>
               <td><?php echo $row['id']; ?></td>
               <td><?php echo $row['name']; ?></td>
               <td><?php echo $row['email']; ?></td>
               <td>
                   <a href="edit.php?id=<?php echo $row['id']; ?>">Edit</a>
                   <a href="delete.php?id=<?php echo $row['id']; ?>">Delete</a>
               </td>
           </tr>
           <?php endwhile; ?>
       </table>
       <a href="create.php">Add New User</a>
   </body>
   </html>
   ```

   **create.php** :
   ```php
   <?php
   if ($_SERVER["REQUEST_METHOD"] == "POST") {
       $mysqli = new mysqli("db", "user", "password", "testdb");

       if ($mysqli->connect_error) {
           die("Connection failed: " . $mysqli->connect_error);
       }

       $name = $_POST['name'];
       $email = $_POST['email'];

       $sql = "INSERT INTO users (name, email) VALUES ('$name', '$email')";

       if ($mysqli->query($sql) === TRUE) {
           header("Location: index.php");
       } else {
           echo "Error: " . $sql . "<br>" . $mysqli->error;
       }

       $mysqli->close();
   }
   ?>

   <!DOCTYPE html>
   <html>
   <head>
       <title>Create User</title>
       <link rel="stylesheet" href="style.css">
   </head>
   <body>
       <h1>Create User</h1>
       <form method="POST" action="">
           <label>Name:</label>
           <input type="text" name="name" required><br>
           <label>Email:</label>
           <input type="email" name="email" required><br>
           <button type="submit">Create</button>
       </form>
       <a href="index.php">Back to Users</a>
   </body>
   </html>
   ```

   **edit.php** :
   ```php
   <?php
   $mysqli = new mysqli("db", "user", "password", "testdb");

   if ($mysqli->connect_error) {
       die("Connection failed: " . $mysqli->connect_error);
   }

   if ($_SERVER["REQUEST_METHOD"] == "POST") {
       $id = $_POST['id'];
       $name = $_POST['name'];
       $email = $_POST['email'];

       $sql = "UPDATE users SET name='$name', email='$email' WHERE id=$id";

       if ($mysqli->query($sql) === TRUE) {
           header("Location: index.php");
       } else {
           echo "Error: " . $sql . "<br>" . $mysqli->error;
       }
   } else {
       $id = $_GET['id'];
       $result = $mysqli->query("SELECT * FROM users WHERE id=$id");
       $user = $result->fetch_assoc();
   }

   $mysqli->close();
   ?>

   <!DOCTYPE html>
   <html>
   <head>
       <title>Edit User</title>
       <link rel="stylesheet" href="style.css">
   </head>
   <body>
       <h1>Edit User</h1>
       <form method="POST" action="">
           <input type="hidden" name="id" value="<?php echo $user['id']; ?>">
           <label>Name:</label>
           <input type="text" name="name" value="<?php echo $user['name']; ?>" required><br>
           <label>Email:</label>
           <input type="email" name="email" value="<?php echo $user['email']; ?>" required><br>
           <button type="submit">Update</button>
       </form>
       <a href="index.php">Back to Users</a>
   </body>
   </html>
   ```

   **delete.php** :
   ```php
   <?php
   $mysqli = new mysqli("db", "user", "password", "testdb");

   if ($mysqli->connect_error) {
       die("Connection failed: " . $mysqli->connect_error);
   }

   $id = $_GET['id'];
   $sql = "DELETE FROM users WHERE id=$id";

   if ($mysqli->query($sql) === TRUE) {
       header("Location: index.php");
   } else {
       echo "Error: " . $sql . "<br>" . $mysqli->error;
   }

   $mysqli->close();
   ?>
   ```

   **style.css** :
   ```css
   body {
       font-family: Arial, sans-serif;
       margin: 0;
       padding: 0;
       background-color: #f4f4f4;
   }

   h1{
       text-align: center;
       margin: 20px 0;
   }

   table {
       width: 80%;
       margin: 20px auto;
       border-collapse: collapse;
   }

   table, th, td {
       border: 1px solid #ddd;
   }

   th, td {
       padding: 8px;
       text-align: center;
   }

   th {
       background-color: #f2f2f2;
   }

   form {
       width: 50%;
       margin: 20px auto;
       padding: 20px;
       background-color: #fff;
       box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
   }

   label {
       display: block;
       margin-bottom: 8px;
   }

   input[type="text"], input[type="email"] {
       width: 100%;
       padding: 8px;
       margin-bottom: 10px;
       border: 1px solid #ccc;
       border-radius: 4px;
   }

   button {
       display: block;
       width: 100%;
       padding: 10px;
       background-color: #5cb85c;
       color: white;
       border: none;
       border-radius: 4px;
       cursor: pointer;
   }

   button:hover {
       background-color: #4cae4c;
   }

   a {
       display: block;
       text-align: center;
       margin-top: 20px;
       color: #337ab7;
       text-decoration: none;
   }

   a:hover {
       text-decoration: underline;
   }
   ```

### Étape 3 : Initialiser la base de données

1. **Créer un script d'initialisation pour la base de données** :
   - Créez un fichier `init.sql` dans le dossier `src` avec le contenu suivant :
     ```sql
     CREATE TABLE IF NOT EXISTS users (
         id INT AUTO_INCREMENT PRIMARY KEY,
         name VARCHAR(255) NOT NULL,
         email VARCHAR(255) NOT NULL
     );
     ```

2. **Ajouter le script au service MySQL dans docker-compose.yml** :
   - Modifiez le service `db` dans `docker-compose.yml` pour inclure le script d'initialisation :
     ```yaml
     db:
       image: mysql:5.7
       restart: always
       environment:
         MYSQL_ROOT_PASSWORD: root
         MYSQL_DATABASE: testdb
         MYSQL_USER: user
         MYSQL_PASSWORD: password
       ports:
         - "3306:3306"
       volumes:
         - ./src/init.sql:/docker-entrypoint-initdb.d/init.sql
         - db_data:/var/lib/mysql
     ```

### Étape 4 : Lancer l'application

1. **Démarrer les conteneurs Docker** :
   - Ouvrez le terminal intégré dans VSCode (`Ctrl+``) et exécutez la commande suivante :
     ```bash
     docker-compose up --build
     ```

2. **Accéder à l'application** :
   - Ouvrez votre navigateur et allez à `http://localhost:8080`.

### Étape 5 : Déployer le conteneur sur un serveur distant

Pour déployer votre application Docker sur un serveur distant, suivez ces étapes :

1. **Configurer votre serveur distant** :
   - Assurez-vous que Docker est installé sur votre serveur distant.
   - Connectez-vous à votre serveur via SSH :
     ```bash
     ssh user@remote_server_ip
     ```

2. **Installer Docker sur le serveur distant** :
   - **Ubuntu** :
     ```bash
     sudo apt update
     sudo apt install apt-transport-https ca-certificates curl software-properties-common
     curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
     sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
     sudo apt update
     sudo apt install docker-ce
     ```
   - **CentOS** :
     ```bash
     sudo yum install -y yum-utils device-mapper-persistent-data lvm2
     sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
     sudo yum install docker-ce
     sudo systemctl start docker
     sudo systemctl enable docker
     ```

3. **Installer Docker Compose sur le serveur distant** :
   - Téléchargez Docker Compose :
     ```bash
     sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
     sudo chmod +x /usr/local/bin/docker-compose
     ```

4. **Transférer les fichiers de votre projet** :
   - Utilisez `scp` pour copier vos fichiers sur le serveur distant :
     ```bash
     scp -r my-php-app user@remote_server_ip:/path/to/deployment/directory
     ```

5. **Démarrer les conteneurs sur le serveur distant** :
   - Connectez-vous à votre serveur distant et naviguez jusqu'au répertoire où vous avez transféré les fichiers.
   - Exécutez les commandes Docker pour démarrer l'application :
     ```bash
     cd /path/to/deployment/directory/my-php-app
     docker-compose up --build -d
     ```

6. **Configurer le firewall et les ports** :
   - Assurez-vous que les ports nécessaires sont ouverts sur votre serveur. Vous pouvez utiliser `ufw` pour configurer le firewall :
     ```bash
     sudo ufw allow 80/tcp
     sudo ufw allow 3306/tcp
     sudo ufw enable
     ```

7. **Accéder à l'application déployée** :
   - Ouvrez votre navigateur et allez à `http://remote_server_ip` pour accéder à votre application déployée.


----

Déployer  l'application sur AWS, nous allons utiliser Amazon Elastic Beanstalk, un service qui facilite le déploiement et la gestion des applications dans le cloud AWS. Elastic Beanstalk gère automatiquement la capacité, le load balancing, le scaling et la surveillance de votre application.

### Étape 1 : Préparation de l'environnement AWS

1. **Créer un compte AWS** :
   - Si vous n'avez pas encore de compte AWS, rendez-vous sur [AWS](https://aws.amazon.com/) et créez un compte.

2. **Configurer AWS CLI** :
   - Installez AWS CLI sur votre machine locale. Suivez les instructions d'installation ici : [AWS CLI Installation](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html).
   - Configurez AWS CLI avec vos identifiants :
     ```bash
     aws configure
     ```
   - Entrez votre AWS Access Key, AWS Secret Access Key, région par défaut (par exemple, `us-west-2`), et le format de sortie par défaut (`json`).

### Étape 2 : Préparer l'application pour Elastic Beanstalk

1. **Créer un fichier Docker pour Elastic Beanstalk** :
   - Elastic Beanstalk utilise un fichier `Dockerrun.aws.json` pour déployer des applications Docker multi-containers. Créez ce fichier à la racine de votre projet avec le contenu suivant :
     ```json
     {
       "AWSEBDockerrunVersion": 2,
       "containerDefinitions": [
         {
           "name": "web",
           "image": "web_image_name",
           "essential": true,
           "memory": 128,
           "portMappings": [
             {
               "containerPort": 80,
               "hostPort": 80
             }
           ],
           "links": ["db"]
         },
         {
           "name": "db",
           "image": "mysql:5.7",
           "essential": true,
           "environment": [
             {
               "name": "MYSQL_ROOT_PASSWORD",
               "value": "root"
             },
             {
               "name": "MYSQL_DATABASE",
               "value": "testdb"
             },
             {
               "name": "MYSQL_USER",
               "value": "user"
             },
             {
               "name": "MYSQL_PASSWORD",
               "value": "password"
             }
           ],
           "memory": 128,
           "portMappings": [
             {
               "containerPort": 3306,
               "hostPort": 3306
             }
           ]
         }
       ]
     }
     ```
   - Remplacez `"web_image_name"` par le nom de votre image Docker pour le service web.

2. **Construire et pousser vos images Docker sur Amazon ECR** :
   - Créez un référentiel Amazon ECR pour stocker vos images Docker. Suivez les instructions ici : [Amazon ECR](https://docs.aws.amazon.com/AmazonECR/latest/userguide/repository-create.html).
   - Authentifiez-vous auprès de votre registre Amazon ECR :
     ```bash
     aws ecr get-login-password --region <your-region> | docker login --username AWS --password-stdin <your-account-id>.dkr.ecr.<your-region>.amazonaws.com
     ```
   - Taggez et poussez votre image Docker vers Amazon ECR :
     ```bash
     docker tag web_image_name:latest <your-account-id>.dkr.ecr.<your-region>.amazonaws.com/web_image_name:latest
     docker push <your-account-id>.dkr.ecr.<your-region>.amazonaws.com/web_image_name:latest
     ```

### Étape 3 : Déployer l'application sur Elastic Beanstalk

1. **Installer EB CLI** :
   - Elastic Beanstalk CLI (EB CLI) simplifie les déploiements. Suivez les instructions d'installation ici : [EB CLI Installation](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3-install.html).

2. **Initialiser Elastic Beanstalk** :
   - À la racine de votre projet, initialisez un nouvel environnement Elastic Beanstalk :
     ```bash
     eb init
     ```
   - Suivez les instructions pour configurer votre application. Sélectionnez votre région et votre plateforme (Docker).

3. **Créer un environnement Elastic Beanstalk** :
   - Créez un nouvel environnement pour votre application :
     ```bash
     eb create my-app-env
     ```

4. **Déployer votre application** :
   - Déployez votre application dans l'environnement Elastic Beanstalk :
     ```bash
     eb deploy
     ```

5. **Vérifier le déploiement** :
   - Une fois le déploiement terminé, vous pouvez accéder à votre application via l'URL fournie par Elastic Beanstalk :
     ```bash
     eb open
     ```
