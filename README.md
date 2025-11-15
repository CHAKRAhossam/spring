# 🏦 Microservice Banque (MsBanque)

## 📋 Description

**MsBanque** est un microservice REST développé avec Spring Boot pour la gestion de comptes bancaires. Ce service permet d'effectuer des opérations CRUD (Create, Read, Update, Delete) sur des comptes bancaires avec support des formats JSON et XML.

### Fonctionnalités principales

- ✅ Gestion complète des comptes bancaires (CRUD)
- ✅ Support des formats JSON et XML
- ✅ Base de données H2 en mémoire
- ✅ Documentation API automatique avec Swagger/OpenAPI
- ✅ Console H2 pour l'inspection de la base de données
- ✅ Architecture RESTful

---

## 🏗️ Architecture

Le projet suit une architecture en couches typique des applications Spring Boot :

```
┌─────────────────────────────────────┐
│      CompteController (REST API)     │
│         /banque/comptes              │
└─────────────────┬───────────────────┘
                  │
┌─────────────────▼───────────────────┐
│    CompteRepository (JPA)           │
│    Interface Spring Data JPA        │
└─────────────────┬───────────────────┘
                  │
┌─────────────────▼───────────────────┐
│         Entity: Compte              │
│    (id, solde, dateCreation, type) │
└─────────────────┬───────────────────┘
                  │
┌─────────────────▼───────────────────┐
│      Base de données H2             │
│      (En mémoire)                   │
└─────────────────────────────────────┘
```

### Structure du projet

```
spring/
├── src/
│   ├── main/
│   │   ├── java/ma/rest/spring/
│   │   │   ├── MsBanqueApplication.java      # Point d'entrée
│   │   │   ├── controllers/
│   │   │   │   └── CompteController.java     # Contrôleur REST
│   │   │   ├── entities/
│   │   │   │   ├── Compte.java               # Entité JPA
│   │   │   │   └── TypeCompte.java           # Enum (COURANT, EPARGNE)
│   │   │   └── repositories/
│   │   │       └── CompteRepository.java     # Repository JPA
│   │   └── resources/
│   │       └── application.properties        # Configuration
│   └── test/
└── pom.xml                                   # Dépendances Maven
```

---

## 🛠️ Technologies utilisées

| Technologie | Version | Description |
|------------|---------|-------------|
| **Spring Boot** | 3.5.7 | Framework principal |
| **Java** | 21 | Langage de programmation |
| **Spring Data JPA** | - | Abstraction pour la persistance |
| **H2 Database** | - | Base de données en mémoire |
| **Lombok** | - | Réduction du code boilerplate |
| **SpringDoc OpenAPI** | 2.1.0 | Documentation API (Swagger) |
| **Jackson XML** | - | Support du format XML |
| **Maven** | - | Gestionnaire de dépendances |

---

## 📦 Prérequis

Avant de commencer, assurez-vous d'avoir installé :

- ☕ **Java 21** ou supérieur
- 🔧 **Maven 3.6+** (ou utilisez le wrapper Maven inclus : `mvnw`)
- 💻 Un IDE (IntelliJ IDEA, Eclipse, VS Code) recommandé
- 🌐 Un client HTTP (Postman, cURL, ou navigateur) pour tester l'API

### Vérification de l'installation

```bash
java -version    # Doit afficher Java 21+
mvn -version     # Doit afficher Maven 3.6+
```

---

## 🚀 Installation et démarrage

### 1. Cloner le projet (si applicable)

```bash
git clone <url-du-repo>
cd spring
```

### 2. Compiler le projet

```bash
# Avec Maven wrapper (Windows)
mvnw.cmd clean install

# Avec Maven wrapper (Linux/Mac)
./mvnw clean install

# Ou avec Maven installé globalement
mvn clean install
```

### 3. Lancer l'application

```bash
# Avec Maven wrapper (Windows)
mvnw.cmd spring-boot:run

# Avec Maven wrapper (Linux/Mac)
./mvnw spring-boot:run

# Ou avec Maven installé globalement
mvn spring-boot:run
```

### 4. Vérifier que l'application est démarrée

L'application démarre sur le port **8082**. Vous devriez voir dans les logs :

```
Started MsBanqueApplication in X.XXX seconds
```

---

## ⚙️ Configuration

Le fichier `application.properties` contient la configuration suivante :

```properties
# Nom de l'application
spring.application.name=spring

# Configuration H2 Database
spring.datasource.url=jdbc:h2:mem:banque
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=

# Configuration JPA
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
spring.jpa.hibernate.ddl-auto=update

# Console H2 (accessible à /h2-console)
spring.h2.console.enabled=true
spring.h2.console.path=/h2-console

# Port du serveur
server.port=8082
```

### Accès à la console H2

Une fois l'application démarrée, vous pouvez accéder à la console H2 pour inspecter la base de données :

- **URL** : http://localhost:8082/h2-console
- **JDBC URL** : `jdbc:h2:mem:banque`
- **Username** : `sa`
- **Password** : (laisser vide)

---

## 📚 Documentation API (Swagger)

Une fois l'application démarrée, accédez à la documentation interactive Swagger :

- **URL Swagger UI** : http://localhost:8082/swagger-ui.html
- **URL OpenAPI JSON** : http://localhost:8082/v3/api-docs

La documentation Swagger permet de :
- 📖 Voir toutes les endpoints disponibles
- 🧪 Tester les endpoints directement depuis le navigateur
- 📋 Consulter les modèles de données

---

## 🔌 Endpoints API

Tous les endpoints sont préfixés par `/banque`.

### Base URL
```
http://localhost:8082/banque
```

### 1. Récupérer tous les comptes

```http
GET /banque/comptes
```

**Réponse** : Liste de tous les comptes (JSON ou XML)

**Exemple avec cURL** :
```bash
curl -X GET http://localhost:8082/banque/comptes
```

**Exemple avec XML** :
```bash
curl -X GET http://localhost:8082/banque/comptes \
  -H "Accept: application/xml"
```

---

### 2. Récupérer un compte par ID

```http
GET /banque/comptes/{id}
```

**Paramètres** :
- `id` (path) : Identifiant du compte

**Réponse** : Compte trouvé (200) ou Not Found (404)

**Exemple** :
```bash
curl -X GET http://localhost:8082/banque/comptes/1
```

---

### 3. Créer un nouveau compte

```http
POST /banque/comptes
```

**Body** (JSON) :
```json
{
  "solde": 5000.0,
  "dateCreation": "2024-01-15",
  "type": "COURANT"
}
```

**Body** (XML) :
```xml
<Compte>
  <solde>5000.0</solde>
  <dateCreation>2024-01-15</dateCreation>
  <type>EPARGNE</type>
</Compte>
```

**Exemple avec JSON** :
```bash
curl -X POST http://localhost:8082/banque/comptes \
  -H "Content-Type: application/json" \
  -d '{
    "solde": 5000.0,
    "dateCreation": "2024-01-15",
    "type": "COURANT"
  }'
```

**Exemple avec XML** :
```bash
curl -X POST http://localhost:8082/banque/comptes \
  -H "Content-Type: application/xml" \
  -d '<Compte>
        <solde>3000.0</solde>
        <dateCreation>2024-01-15</dateCreation>
        <type>EPARGNE</type>
      </Compte>'
```

---

### 4. Mettre à jour un compte

```http
PUT /banque/comptes/{id}
```

**Paramètres** :
- `id` (path) : Identifiant du compte à mettre à jour

**Body** (JSON) :
```json
{
  "solde": 7500.0,
  "dateCreation": "2024-01-15",
  "type": "EPARGNE"
}
```

**Exemple** :
```bash
curl -X PUT http://localhost:8082/banque/comptes/1 \
  -H "Content-Type: application/json" \
  -d '{
    "solde": 7500.0,
    "dateCreation": "2024-01-15",
    "type": "EPARGNE"
  }'
```

---

### 5. Supprimer un compte

```http
DELETE /banque/comptes/{id}
```

**Paramètres** :
- `id` (path) : Identifiant du compte à supprimer

**Réponse** : 200 OK si supprimé, 404 si non trouvé

**Exemple** :
```bash
curl -X DELETE http://localhost:8082/banque/comptes/1
```

---

## 📊 Modèle de données

### Entité Compte

```java
{
  "id": Long,              // Identifiant unique (auto-généré)
  "solde": double,         // Solde du compte
  "dateCreation": Date,    // Date de création
  "type": TypeCompte       // Type de compte (COURANT ou EPARGNE)
}
```

### Enum TypeCompte

- `COURANT` : Compte courant
- `EPARGNE` : Compte épargne

---

## 🧪 Données initiales

L'application crée automatiquement 3 comptes de démonstration au démarrage grâce au `CommandLineRunner` dans `MsBanqueApplication.java` :

- Compte 1 : Type EPARGNE, solde aléatoire
- Compte 2 : Type COURANT, solde aléatoire
- Compte 3 : Type EPARGNE, solde aléatoire

---

## 📝 Exemples d'utilisation

### Exemple 1 : Récupérer tous les comptes

```bash
curl http://localhost:8082/banque/comptes
```

**Réponse** :
```json
[
  {
    "id": 1,
    "solde": 4523.45,
    "dateCreation": "2024-01-15",
    "type": "EPARGNE"
  },
  {
    "id": 2,
    "solde": 7890.12,
    "dateCreation": "2024-01-15",
    "type": "COURANT"
  }
]
```

### Exemple 2 : Créer un compte avec Postman

1. Méthode : `POST`
2. URL : `http://localhost:8082/banque/comptes`
3. Headers : `Content-Type: application/json`
4. Body (raw JSON) :
```json
{
  "solde": 10000.0,
  "dateCreation": "2024-01-20",
  "type": "COURANT"
}
```

### Exemple 3 : Mettre à jour un compte

```bash
curl -X PUT http://localhost:8082/banque/comptes/1 \
  -H "Content-Type: application/json" \
  -d '{"solde": 15000.0, "dateCreation": "2024-01-15", "type": "COURANT"}'
```

---

## 🧩 Tests

Pour exécuter les tests :

```bash
mvnw test
# ou
mvn test
```

---

## 🐛 Dépannage

### Problème : Port 8082 déjà utilisé

**Solution** : Modifiez le port dans `application.properties` :
```properties
server.port=8083
```

### Problème : Erreur de compilation Lombok

**Solution** : Assurez-vous que l'annotation processing est activé dans votre IDE :
- IntelliJ IDEA : Settings → Build → Compiler → Annotation Processors → ✅ Enable annotation processing

### Problème : Base de données vide après redémarrage

**Explication** : H2 est une base de données en mémoire. Les données sont perdues à chaque arrêt de l'application. Pour persister les données, configurez une base de données externe (MySQL, PostgreSQL, etc.).

---

## 🔄 Migration vers une base de données persistante

Pour utiliser une base de données persistante (ex: MySQL), modifiez `application.properties` :

```properties
# MySQL Configuration
spring.datasource.url=jdbc:mysql://localhost:3306/banque
spring.datasource.username=root
spring.datasource.password=yourpassword
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.jpa.database-platform=org.hibernate.dialect.MySQLDialect
```

Et ajoutez la dépendance MySQL dans `pom.xml` :
```xml
<dependency>
    <groupId>com.mysql</groupId>
    <artifactId>mysql-connector-j</artifactId>
</dependency>
```

---

## 📹 Vidéo explicative

### Script pour la vidéo explicative

#### **Partie 1 : Introduction (0:00 - 0:30)**
- Présentation du projet MsBanque
- Objectif : microservice REST pour la gestion de comptes bancaires
- Technologies principales utilisées

#### **Partie 2 : Architecture du projet (0:30 - 2:00)**
- Structure des dossiers
- Explication des couches :
  - **Controller** : Point d'entrée REST
  - **Repository** : Accès aux données
  - **Entity** : Modèle de données
- Diagramme de l'architecture

#### **Partie 3 : Configuration et démarrage (2:00 - 3:30)**
- Vérification des prérequis (Java 21, Maven)
- Compilation du projet avec `mvnw clean install`
- Démarrage avec `mvnw spring-boot:run`
- Vérification du démarrage sur le port 8082

#### **Partie 4 : Exploration de la base de données (3:30 - 4:30)**
- Accès à la console H2 : http://localhost:8082/h2-console
- Connexion à la base de données
- Visualisation des comptes créés automatiquement
- Structure de la table `Compte`

#### **Partie 5 : Documentation Swagger (4:30 - 5:30)**
- Accès à Swagger UI : http://localhost:8082/swagger-ui.html
- Navigation dans la documentation
- Visualisation des endpoints disponibles
- Test d'un endpoint directement depuis Swagger

#### **Partie 6 : Tests des endpoints REST (5:30 - 10:00)**
- **GET /banque/comptes** : Récupérer tous les comptes (JSON et XML)
- **GET /banque/comptes/{id}** : Récupérer un compte spécifique
- **POST /banque/comptes** : Créer un nouveau compte (démonstration JSON et XML)
- **PUT /banque/comptes/{id}** : Mettre à jour un compte
- **DELETE /banque/comptes/{id}** : Supprimer un compte
- Utilisation de Postman ou cURL pour les démonstrations

#### **Partie 7 : Code source (10:00 - 12:00)**
- Explication du `CompteController.java` :
  - Annotations REST (@RestController, @RequestMapping)
  - Méthodes CRUD
  - Support JSON/XML
- Explication de l'entité `Compte.java` :
  - Annotations JPA (@Entity, @Id, @GeneratedValue)
  - Utilisation de Lombok
- Explication du `CompteRepository.java` :
  - Interface Spring Data JPA
  - Méthodes héritées automatiquement

#### **Partie 8 : Points importants et bonnes pratiques (12:00 - 13:00)**
- Architecture en couches
- Séparation des responsabilités
- Support multi-format (JSON/XML)
- Gestion des erreurs (404 Not Found)
- Utilisation de Lombok pour réduire le code

#### **Partie 9 : Conclusion (13:00 - 13:30)**
- Résumé des fonctionnalités
- Cas d'usage possibles
- Extensions futures possibles
- Ressources pour aller plus loin

### Outils recommandés pour la vidéo

- 🎥 **OBS Studio** ou **Camtasia** pour l'enregistrement
- 🖥️ **Postman** ou **Thunder Client** pour tester les API
- 📝 **Draw.io** ou **Excalidraw** pour les diagrammes
- 🎨 **Canva** pour les slides d'introduction

### Durée estimée : 13-15 minutes

---

## 🚀 Améliorations futures possibles

- [ ] Ajout de la validation des données (Bean Validation)
- [ ] Gestion des exceptions personnalisées
- [ ] Ajout de tests unitaires et d'intégration
- [ ] Sécurisation avec Spring Security
- [ ] Ajout de la pagination pour les listes
- [ ] Support de la recherche/filtrage
- [ ] Migration vers une base de données persistante
- [ ] Ajout de logs structurés
- [ ] Configuration Docker pour le déploiement
- [ ] Intégration avec d'autres microservices

---

## 📖 Ressources

- [Documentation Spring Boot](https://spring.io/projects/spring-boot)
- [Spring Data JPA](https://spring.io/projects/spring-data-jpa)
- [Documentation H2 Database](https://www.h2database.com/html/main.html)
- [SpringDoc OpenAPI](https://springdoc.org/)
- [Lombok](https://projectlombok.org/)

---

## 👤 Auteur

Développé dans le cadre d'un projet de microservices avec Spring Boot.

---

## 📄 Licence

Ce projet est fourni à des fins éducatives.

---

## 🤝 Contribution

Les contributions sont les bienvenues ! N'hésitez pas à ouvrir une issue ou une pull request.

---

**⭐ Si ce projet vous a été utile, n'hésitez pas à lui donner une étoile !**

