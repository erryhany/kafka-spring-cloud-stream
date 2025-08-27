# 🚀 Kafka Spring Cloud Stream

[![Status](https://img.shields.io/badge/Status-En%20développement-orange)](https://github.com/votre-username/kafka-spring-cloud-stream)
[![Progress](https://img.shields.io/badge/Progress-50%25-yellow)](https://github.com/votre-username/kafka-spring-cloud-stream)
[![Java](https://img.shields.io/badge/Java-21+-red)](https://openjdk.org/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.5.4-green)](https://spring.io/projects/spring-boot)
[![Kafka](https://img.shields.io/badge/Apache%20Kafka-7.3.0-black)](https://kafka.apache.org/)

## 📋 Description

Projet de démonstration et d'apprentissage des technologies de streaming de données avec Apache Kafka, Spring Cloud Stream et Spring Boot. Ce projet illustre la mise en place d'une architecture de streaming de données moderne et scalable.

## 🚀 Fonctionnalités

- **Streaming de données en temps réel** : Traitement de flux de données avec Kafka
- **Spring Cloud Stream** : Abstraction pour le développement de microservices de streaming
- **Kafka Streams** : Traitement de données en temps réel avec Apache Kafka
- **Architecture événementielle** : Communication asynchrone entre services
- **Docker Compose** : Infrastructure Kafka prête à l'emploi
- **Tests intégrés** : Tests avec Spring Cloud Stream Test Binder
- **Monitoring et observabilité** : Suivi des flux de données

## 🛠️ Technologies utilisées

- **Java 21+** - Langage principal avec les dernières fonctionnalités
- **Spring Boot 3.5.4** - Framework principal
- **Spring Cloud Stream 2025.0.0** - Framework de streaming
- **Apache Kafka 7.3.0** - Plateforme de streaming distribuée
- **Kafka Streams** - API de traitement de flux de données
- **Spring Kafka** - Intégration Spring avec Kafka
- **Docker Compose** - Orchestration des services Kafka
- **Lombok** - Réduction du code boilerplate
- **Maven** - Gestion des dépendances

## 📊 État du Projet

**Statut :** 🟡 En développement  
**Progression :** 50%  
**Dernière mise à jour :** Décembre 2024  

### ✅ Ce qui est terminé
- [x] Configuration de base Spring Boot 3.5.4
- [x] Configuration Spring Cloud Stream
- [x] Intégration Apache Kafka
- [x] Configuration Docker Compose pour Kafka
- [x] Dépendances Maven configurées
- [x] Structure du projet
- [x] Configuration Kafka Streams
- [x] Tests avec Spring Cloud Stream Test Binder

### 🚧 En cours de développement
- [ ] Implémentation des streams de données
- [ ] Logique de traitement des événements
- [ ] Configuration des topics Kafka
- [ ] Gestion des erreurs et retry

### 📋 À faire
- [ ] Exemples de streams de données
- [ ] Tests d'intégration avec Kafka
- [ ] Monitoring et métriques
- [ ] Documentation des streams
- [ ] Exemples d'utilisation
- [ ] Optimisation des performances
- [ ] Déploiement en production

## 🚀 Installation et démarrage

### Prérequis
- Java 21 ou supérieur
- Maven 3.6+
- Docker et Docker Compose

### Étapes d'installation

1. **Cloner le projet**
   ```bash
   git clone [URL_DE_VOTRE_DEPOT]
   cd kafka-spring-cloud-stream
   ```

2. **Démarrer l'infrastructure Kafka**
   ```bash
   docker-compose up -d
   ```

3. **Vérifier que Kafka est démarré**
   ```bash
   docker ps
   # Vérifier que zookeeper et kafka-broker sont en cours d'exécution
   ```

4. **Installer les dépendances**
   ```bash
   mvn clean install
   ```

5. **Lancer l'application**
   ```bash
   mvn spring-boot:run
   ```

## 🐳 Infrastructure Docker

Le projet inclut un fichier `compose.yaml` qui démarre automatiquement :

- **Zookeeper** : Service de coordination pour Kafka
- **Kafka Broker** : Serveur Kafka principal
- **Ports exposés** : 9092 pour Kafka, 2181 pour Zookeeper

### Commandes Docker utiles

```bash
# Démarrer les services
docker-compose up -d

# Arrêter les services
docker-compose down

# Voir les logs
docker-compose logs -f

# Redémarrer un service spécifique
docker-compose restart kafka-broker
```

## 📚 Architecture du Projet

```
src/
├── main/
│   ├── java/           # Code source Java
│   └── resources/      # Configuration
├── test/               # Tests
└── compose.yaml        # Infrastructure Docker
```

## 🔄 Spring Cloud Stream

Spring Cloud Stream fournit une abstraction pour le développement de microservices de streaming :

- **Binder** : Interface entre l'application et le système de messaging
- **Source** : Production de messages
- **Sink** : Consommation de messages
- **Processor** : Traitement de messages

## 📊 Kafka Streams

Kafka Streams permet de :

- **Traiter des flux de données** en temps réel
- **Effectuer des agrégations** et des jointures
- **Gérer l'état** des applications de streaming
- **Assurer la scalabilité** et la tolérance aux pannes

## 🧪 Tests

```bash
# Exécuter tous les tests
mvn test

# Tests avec Spring Cloud Stream Test Binder
mvn test -Dtest=StreamingTests

# Tests d'intégration Kafka
mvn test -Dtest=KafkaIntegrationTests
```

## 📈 Monitoring

- **Kafka Manager** : Interface web pour gérer Kafka
- **JMX Metrics** : Métriques Java Management Extensions
- **Spring Boot Actuator** : Endpoints de monitoring (à implémenter)

## 🔧 Configuration

### Propriétés Kafka importantes

```yaml
spring:
  cloud:
    stream:
      kafka:
        binder:
          brokers: localhost:9092
          zk-nodes: localhost:2181
      bindings:
        input:
          destination: input-topic
        output:
          destination: output-topic
```

## 📝 Contribution

1. Fork le projet
2. Créer une branche pour votre fonctionnalité
3. Commiter vos changements
4. Pousser vers la branche
5. Ouvrir une Pull Request

## 📄 Licence

Ce projet est sous licence [MIT](LICENSE).

## 👨‍💻 Auteur

**Mourad** - Développeur Full Stack

## 📞 Support

Pour toute question ou suggestion, n'hésitez pas à :
- Ouvrir une issue sur GitHub
- Me contacter directement

## 🔗 Ressources utiles

- [Spring Cloud Stream Documentation](https://spring.io/projects/spring-cloud-stream)
- [Apache Kafka Documentation](https://kafka.apache.org/documentation/)
- [Kafka Streams Documentation](https://kafka.apache.org/documentation/streams/)

---

**Note :** Ce projet est actuellement en développement actif. Les fonctionnalités peuvent évoluer et certaines parties peuvent ne pas être encore implémentées.
