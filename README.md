#   TP3: Mise en place d'un cluster de 2 nodes
#   Description
Ce projet consiste en la mise en place d'un cluster de 2 machines virtuelles (VM) configurées via Vagrant.

Ces machines seront utilisées pour déployer une application Spring Boot sur le serveur web et une base de données MySQL sur le serveur db.

#   Prérequis
Avant de commencer, assurez-vous d'avoir installé les outils suivants :

    Vagrant
    VirtualBox
    Node.js

1. Création des machines virtuelles

Créez 2 dossiers pour les machines : web et db.

![V](cap1.png)

Utilisez Vagrant pour configurer les machines virtuelles

Execute sur chaque fichier pour creer le fichier vagrantfile:

```bash
vagrant init
```
#   - Pour db:

![V](c2.png)

#   - Pour web:

![V](c3.png)

2. Configuration des machines et demarrage:

Pour Web:

![V](c4.png)

Execute :

```bash
vagrant validate
vagrant up

```
![V](c6.png)

Pour db:

![V](c4.png)

Execute :
```bash
vagrant validate
vagrant up

```

![K8S](c7.png)

3. Démarrage de la VM:

![K8S](c8.png)

4. Clonez le projet Spring Boot sur la machine web ::

```bash
git clone https://github.com/ngorseck/admin-app.git
cd admin-app

```
![K8S](c9.png)

Resultat:

![K8S](c10.png)

4. Changez le port en 8086 pour démarrer un serveur sur le port 8086:

![K8S](c23.png)


5. Configuration la machine Web:

Sur la machine Web: :

```bash
sudo apt update

```
![K8S](c13.png)

Installez Node.js sur la machine web :

```bash
curl -fsSL https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.4/install.sh | bash
nvm install --lts
nvm use --lts

```

Vérifiez l'installation :

```bash
node -v
npm -v
```

![K8S](c14.png)

6.Test de l'interconnexion

Ping entre les machines :

```bash
ping 192.168.33.10  # Depuis web vers db
ping 192.168.33.11  # Depuis db vers web
```

![K8S](c15.png)

7.Installer:

Sur la machine Web, installer jdk la version 17:

```bash
sudo apt install -y openjdk-17-jdk
```
![K8S](c16.png)

Sur la machine Web, installer git:

![K8S](c18.png)

Sur la machine Web, installer maven:

```bash
sudo apt update
sudo apt install -y maven
```
![K8S](c20.png)

7. Configuration de la base de données MySQL :

Sur la machine db :

```bash

sudo apt update
sudo apt install mysql-server -y

```

![K8S](c12.png)

![K8S](c11.png)

Créer la base de données : Connectez-vous à MySQL en tant qu'utilisateur root :

![K8S](c17.png)

Maintenant on crée un utilisateur:

```bash
CREATE USER 'user'@'%' IDENTIFIED BY 'user123'; 
```
![K8S](c19.png)

```bash
grant all privileges on adminapp_db.* to 'user'@'%' with grant option;
FLUSH PRIVILEGES;
```

![K8S](c21.png)

8. Configurer votre application.yml:

![K8S](c23.png)

![K8S](c24.png)

8. Déployer votre application:
9. 
```bash
mvn spring-boot:run -DskipTests
```
![K8S](c22.png)

Testons notre application sur postman:

![K8S](c25.png)

![K8S](c26.png)

![K8S](c27.png)







