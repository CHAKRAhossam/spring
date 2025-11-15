# 🎬 Script détaillé pour la vidéo explicative - MsBanque

## 📋 Informations générales

- **Durée totale** : 13-15 minutes
- **Public cible** : Développeurs débutants à intermédiaires en Spring Boot
- **Objectif** : Comprendre l'architecture et l'utilisation du microservice MsBanque

---

## 🎥 Plan de la vidéo

### **Séquence 1 : Introduction et présentation (0:00 - 1:00)**

**Visuel** :
- Slide d'introduction avec logo Spring Boot
- Titre : "Microservice Banque - MsBanque"
- Capture d'écran de la structure du projet

**Narration** :
> "Bonjour et bienvenue dans cette vidéo explicative du projet MsBanque. MsBanque est un microservice REST développé avec Spring Boot pour la gestion de comptes bancaires. Dans cette vidéo, nous allons explorer l'architecture du projet, voir comment le démarrer, et tester toutes les fonctionnalités disponibles."

**Actions** :
- Montrer la structure du projet dans l'IDE
- Présenter les technologies utilisées

---

### **Séquence 2 : Architecture et structure du projet (1:00 - 3:00)**

**Visuel** :
- Diagramme d'architecture (à créer avec Draw.io)
- Navigation dans les dossiers du projet
- Affichage de la structure des packages

**Narration** :
> "Commençons par comprendre l'architecture du projet. MsBanque suit une architecture en couches classique. Nous avons trois couches principales : le contrôleur REST qui expose les endpoints, le repository qui gère l'accès aux données, et l'entité qui représente notre modèle de données. La base de données H2 stocke les informations en mémoire."

**Actions** :
- Ouvrir le package `controllers` → montrer `CompteController.java`
- Ouvrir le package `repositories` → montrer `CompteRepository.java`
- Ouvrir le package `entities` → montrer `Compte.java` et `TypeCompte.java`
- Expliquer le flux : Controller → Repository → Entity → Database

**Diagramme à afficher** :
```
Controller (REST) → Repository (JPA) → Entity → H2 Database
```

---

### **Séquence 3 : Configuration et démarrage (3:00 - 5:00)**

**Visuel** :
- Terminal/Console ouverte
- Fichier `application.properties` ouvert
- Logs de démarrage de l'application

**Narration** :
> "Avant de démarrer l'application, vérifions la configuration. Le fichier application.properties contient toutes les configurations nécessaires : la base de données H2, le port du serveur sur 8082, et l'activation de la console H2. Pour démarrer l'application, nous utilisons Maven avec la commande `mvnw spring-boot:run`."

**Actions** :
1. Ouvrir `application.properties` et expliquer chaque ligne
2. Dans le terminal, exécuter :
   ```bash
   mvnw clean install
   ```
3. Puis :
   ```bash
   mvnw spring-boot:run
   ```
4. Montrer les logs de démarrage
5. Vérifier que l'application démarre sur le port 8082

**Points clés à mentionner** :
- Port 8082
- Base de données H2 en mémoire
- Console H2 activée
- Données initiales créées automatiquement

---

### **Séquence 4 : Exploration de la base de données H2 (5:00 - 6:30)**

**Visuel** :
- Navigateur ouvert sur http://localhost:8082/h2-console
- Interface de connexion H2
- Résultats de la requête SQL

**Narration** :
> "Une fois l'application démarrée, nous pouvons accéder à la console H2 pour inspecter la base de données. L'URL est http://localhost:8082/h2-console. Nous nous connectons avec les identifiants par défaut : username 'sa' et pas de mot de passe. Ensuite, nous pouvons exécuter une requête SQL pour voir les comptes créés automatiquement au démarrage."

**Actions** :
1. Ouvrir le navigateur
2. Aller sur http://localhost:8082/h2-console
3. Remplir les champs de connexion :
   - JDBC URL : `jdbc:h2:mem:banque`
   - Username : `sa`
   - Password : (vide)
4. Cliquer sur "Connect"
5. Exécuter la requête : `SELECT * FROM COMPTE;`
6. Montrer les résultats (3 comptes avec des soldes aléatoires)

---

### **Séquence 5 : Documentation Swagger (6:30 - 8:00)**

**Visuel** :
- Navigateur ouvert sur Swagger UI
- Navigation dans l'interface Swagger
- Test d'un endpoint depuis Swagger

**Narration** :
> "SpringDoc OpenAPI génère automatiquement une documentation interactive de notre API. Accédons à Swagger UI sur http://localhost:8082/swagger-ui.html. Ici, nous pouvons voir tous nos endpoints, leurs paramètres, et même les tester directement depuis le navigateur."

**Actions** :
1. Ouvrir http://localhost:8082/swagger-ui.html
2. Montrer la liste des endpoints disponibles
3. Cliquer sur "GET /banque/comptes"
4. Cliquer sur "Try it out"
5. Cliquer sur "Execute"
6. Montrer la réponse JSON avec la liste des comptes
7. Expliquer que Swagger supporte aussi XML

**Points clés** :
- Documentation automatique
- Test interactif des endpoints
- Support JSON et XML visible dans Swagger

---

### **Séquence 6 : Tests des endpoints REST - Partie 1 : GET (8:00 - 9:30)**

**Visuel** :
- Postman ou Thunder Client ouvert
- Requêtes HTTP affichées
- Réponses JSON/XML affichées

**Narration** :
> "Maintenant, testons nos endpoints REST avec Postman. Commençons par récupérer tous les comptes avec une requête GET. Nous pouvons demander la réponse en JSON ou en XML en spécifiant l'en-tête Accept."

**Actions** :
1. **GET /banque/comptes (JSON)** :
   - Méthode : GET
   - URL : http://localhost:8082/banque/comptes
   - Headers : `Accept: application/json`
   - Envoyer la requête
   - Montrer la réponse JSON

2. **GET /banque/comptes (XML)** :
   - Même URL
   - Headers : `Accept: application/xml`
   - Envoyer la requête
   - Montrer la réponse XML

3. **GET /banque/comptes/{id}** :
   - URL : http://localhost:8082/banque/comptes/1
   - Montrer la réponse avec un seul compte
   - Tester avec un ID inexistant pour montrer le 404

---

### **Séquence 7 : Tests des endpoints REST - Partie 2 : POST (9:30 - 11:00)**

**Visuel** :
- Postman avec requête POST
- Body JSON et XML
- Réponse avec le compte créé

**Narration** :
> "Créons maintenant un nouveau compte avec une requête POST. Nous pouvons envoyer les données en JSON ou en XML. Le compte sera créé et nous recevrons la réponse avec l'ID généré automatiquement."

**Actions** :
1. **POST /banque/comptes (JSON)** :
   - Méthode : POST
   - URL : http://localhost:8082/banque/comptes
   - Headers : `Content-Type: application/json`
   - Body (raw JSON) :
     ```json
     {
       "solde": 10000.0,
       "dateCreation": "2024-01-20",
       "type": "COURANT"
     }
     ```
   - Envoyer et montrer la réponse

2. **POST /banque/comptes (XML)** :
   - Même URL
   - Headers : `Content-Type: application/xml`
   - Body (raw XML) :
     ```xml
     <Compte>
       <solde>5000.0</solde>
       <dateCreation>2024-01-20</dateCreation>
       <type>EPARGNE</type>
     </Compte>
     ```
   - Envoyer et montrer la réponse

3. Vérifier dans H2 console que le compte a été créé

---

### **Séquence 8 : Tests des endpoints REST - Partie 3 : PUT et DELETE (11:00 - 12:30)**

**Visuel** :
- Postman avec requêtes PUT et DELETE
- Avant/après dans la base de données

**Narration** :
> "Mettons à jour un compte existant avec PUT, puis supprimons-le avec DELETE. Ces opérations modifient l'état de notre base de données."

**Actions** :
1. **PUT /banque/comptes/{id}** :
   - Méthode : PUT
   - URL : http://localhost:8082/banque/comptes/1
   - Headers : `Content-Type: application/json`
   - Body :
     ```json
     {
       "solde": 15000.0,
       "dateCreation": "2024-01-15",
       "type": "EPARGNE"
     }
     ```
   - Envoyer et montrer la réponse
   - Vérifier dans H2 que le solde a été mis à jour

2. **DELETE /banque/comptes/{id}** :
   - Méthode : DELETE
   - URL : http://localhost:8082/banque/comptes/1
   - Envoyer la requête
   - Montrer le code de réponse 200 OK
   - Vérifier dans H2 que le compte a été supprimé
   - Tester avec un ID inexistant pour montrer le 404

---

### **Séquence 9 : Exploration du code source (12:30 - 14:00)**

**Visuel** :
- IDE avec les fichiers Java ouverts
- Code source avec annotations mises en évidence

**Narration** :
> "Explorons maintenant le code source pour comprendre comment tout cela fonctionne. Commençons par le contrôleur qui expose nos endpoints REST."

**Actions** :
1. **CompteController.java** :
   - Montrer l'annotation `@RestController`
   - Expliquer `@RequestMapping("/banque")`
   - Parcourir chaque méthode :
     - `@GetMapping` pour GET
     - `@PostMapping` pour POST
     - `@PutMapping` pour PUT
     - `@DeleteMapping` pour DELETE
   - Expliquer `produces` et `consumes` pour JSON/XML
   - Montrer la gestion des erreurs avec `ResponseEntity`

2. **Compte.java** :
   - Montrer les annotations JPA : `@Entity`, `@Id`, `@GeneratedValue`
   - Expliquer les annotations Lombok : `@Data`, `@NoArgsConstructor`, `@AllArgsConstructor`
   - Montrer les champs : id, solde, dateCreation, type

3. **CompteRepository.java** :
   - Montrer que c'est une interface qui étend `JpaRepository`
   - Expliquer que Spring génère automatiquement les méthodes CRUD

4. **MsBanqueApplication.java** :
   - Montrer le `CommandLineRunner` qui crée les données initiales
   - Expliquer le `@Bean` et l'injection de dépendance

---

### **Séquence 10 : Points importants et bonnes pratiques (14:00 - 15:00)**

**Visuel** :
- Slides avec les points clés
- Code source avec annotations

**Narration** :
> "Pour conclure, voici les points importants à retenir de ce projet. L'architecture en couches permet une séparation claire des responsabilités. Le support multi-format JSON/XML rend l'API flexible. L'utilisation de Lombok réduit considérablement le code boilerplate. Et Spring Data JPA simplifie l'accès aux données."

**Points à afficher** :
- ✅ Architecture en couches (Controller → Repository → Entity)
- ✅ Support JSON et XML
- ✅ Utilisation de Lombok pour réduire le code
- ✅ Spring Data JPA pour simplifier l'accès aux données
- ✅ Documentation automatique avec Swagger
- ✅ Base de données H2 pour le développement rapide

---

### **Séquence 11 : Conclusion et ressources (15:00 - 15:30)**

**Visuel** :
- Slide de conclusion
- Liens vers les ressources

**Narration** :
> "Merci d'avoir suivi cette vidéo ! Vous avez maintenant une bonne compréhension du microservice MsBanque. N'hésitez pas à explorer le code, à tester les endpoints, et à consulter le README pour plus de détails. Les liens vers les ressources sont disponibles dans la description de la vidéo."

**Actions** :
- Afficher les liens vers :
  - Documentation Spring Boot
  - Documentation Spring Data JPA
  - Documentation H2
  - Repository GitHub (si applicable)
- Remercier les viewers
- Inviter à s'abonner pour plus de contenu

---

## 🎨 Éléments visuels à préparer

### Slides d'introduction
- Logo Spring Boot
- Titre du projet
- Technologies utilisées (icônes)

### Diagrammes
- Architecture en couches (Draw.io ou Excalidraw)
- Flux de données (Controller → Repository → Entity → DB)

### Captures d'écran
- Structure du projet dans l'IDE
- Console H2 avec les données
- Swagger UI
- Postman avec les requêtes

---

## 🎬 Conseils pour l'enregistrement

1. **Préparation** :
   - Tester toutes les requêtes avant l'enregistrement
   - Préparer les données de test
   - Vérifier que l'application démarre correctement

2. **Qualité audio** :
   - Utiliser un bon microphone
   - Enregistrer dans un environnement calme
   - Parler clairement et à un rythme modéré

3. **Qualité vidéo** :
   - Résolution minimale : 1080p
   - Zoom sur les zones importantes
   - Utiliser des transitions fluides

4. **Édition** :
   - Ajouter des annotations pour mettre en évidence
   - Ajouter de la musique d'ambiance (optionnel)
   - Ajouter des sous-titres (recommandé)

5. **Rythme** :
   - Ne pas aller trop vite
   - Faire des pauses entre les sections
   - Répéter les points importants

---

## 📝 Checklist avant publication

- [ ] Toutes les requêtes fonctionnent correctement
- [ ] Les URLs sont correctes
- [ ] Les exemples de code sont testés
- [ ] La qualité audio est bonne
- [ ] La qualité vidéo est bonne
- [ ] Les sous-titres sont ajoutés (optionnel mais recommandé)
- [ ] La description de la vidéo contient les liens vers les ressources
- [ ] Les timestamps sont ajoutés dans la description

---

**Bonne chance pour votre enregistrement ! 🎥**

