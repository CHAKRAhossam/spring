# Microservice Banque (MsBanque)

## Description

MsBanque est un microservice REST développé avec Spring Boot pour la gestion de comptes bancaires. Ce service permet d'effectuer des opérations CRUD sur des comptes bancaires avec support des formats JSON et XML.

## Technologies

- Spring Boot 3.5.7
- Java 21
- Spring Data JPA
- H2 Database (en mémoire)
- Lombok
- SpringDoc OpenAPI (Swagger)
- Maven

## Prérequis

- Java 21 ou supérieur
- Maven 3.6+ (ou wrapper Maven inclus)

## Installation et démarrage

### Compiler le projet

```bash
# Windows
mvnw.cmd clean install

# Linux/Mac
./mvnw clean install
```

### Lancer l'application

```bash
# Windows
mvnw.cmd spring-boot:run

# Linux/Mac
./mvnw spring-boot:run
```

L'application démarre sur le port **8082**.

## Configuration

Le fichier `application.properties` contient la configuration de la base de données H2 et du serveur.

- Port : 8082
- Console H2 : http://localhost:8082/h2-console
- Swagger UI : http://localhost:8082/swagger-ui.html

## Endpoints API

Base URL : `http://localhost:8082/banque`

### GET /banque/comptes
Récupère tous les comptes (JSON ou XML)

```bash
curl http://localhost:8082/banque/comptes
```

### GET /banque/comptes/{id}
Récupère un compte par son identifiant

```bash
curl http://localhost:8082/banque/comptes/1
```

### POST /banque/comptes
Crée un nouveau compte

```bash
curl -X POST http://localhost:8082/banque/comptes \
  -H "Content-Type: application/json" \
  -d '{
    "solde": 5000.0,
    "dateCreation": "2024-01-15",
    "type": "COURANT"
  }'
```

### PUT /banque/comptes/{id}
Met à jour un compte existant

```bash
curl -X PUT http://localhost:8082/banque/comptes/1 \
  -H "Content-Type: application/json" \
  -d '{
    "solde": 7500.0,
    "dateCreation": "2024-01-15",
    "type": "EPARGNE"
  }'
```

### DELETE /banque/comptes/{id}
Supprime un compte

```bash
curl -X DELETE http://localhost:8082/banque/comptes/1
```

## Structure du projet

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

## Modèle de données

### Compte

```json
{
  "id": Long,
  "solde": double,
  "dateCreation": Date,
  "type": "COURANT" | "EPARGNE"
}
```

## Vidéo explicative


https://github.com/user-attachments/assets/dfcc459a-6632-495d-8cdf-ae3d30d339c1



