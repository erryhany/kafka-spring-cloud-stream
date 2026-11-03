# Kafka Spring Cloud Stream — analytics de pages en temps réel

Pipeline de streaming événementiel avec **Apache Kafka**, **Spring Cloud Stream** et **Kafka Streams**. L'application produit des événements de visite de pages et les agrège sur des fenêtres de 5 secondes. Les résultats sont affichés en direct dans un graphique alimenté par **Server-Sent Events**.

![Java](https://img.shields.io/badge/Java-21-red)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.5-green)
![Spring Cloud Stream](https://img.shields.io/badge/Spring%20Cloud%20Stream-2025.0-6DB33F)
![Kafka](https://img.shields.io/badge/Apache%20Kafka-Streams-231F20)

## Architecture du flux

```
                 pageEventSupplier (toutes les 200 ms)
                              │
                              ▼
 GET /publish ──────▶  topic T3  ──▶  KStreamFunction (Kafka Streams)
 (topic au choix)                      • filtre : durée > 100 ms
        │                              • regroupement par page
        ▼                              • comptage sur fenêtre de 5 s
   topic T2                                       │
        │                             ┌───────────┴───────────┐
        ▼                             ▼                       ▼
 pageEventConsumer                topic T4         state store "count-store"
 (affiche l'événement)                                        │
                                                              ▼
                                            GET /analytics (SSE, chaque seconde)
                                                              │
                                                              ▼
                                            index.html : graphique temps réel
```

## Ce que montre le projet

- **Programmation fonctionnelle Spring Cloud Stream** : beans `Supplier`, `Consumer` et `Function` liés à des topics Kafka par configuration
- **Producteur à la demande** avec `StreamBridge`, vers n'importe quel topic
- **Kafka Streams** : `filter`, `map`, `groupByKey` et agrégation sur fenêtres de temps (`TimeWindows`)
- **Interactive Queries** : lecture du state store `count-store` depuis un contrôleur REST
- **Streaming réactif vers le navigateur** : `Flux` de Project Reactor exposé en `text/event-stream`
- **Infrastructure conteneurisée** : Kafka (mode KRaft) et Kafka UI avec Docker Compose

## Stack technique

| Couche | Technologies |
|---|---|
| Langage | Java 21 (records) |
| Framework | Spring Boot 3.5, Spring Cloud Stream 2025.0 |
| Messaging | Apache Kafka 3.8 (KRaft, sans Zookeeper), Kafka Streams |
| Temps réel | Server-Sent Events, Project Reactor |
| Front | HTML + Smoothie Charts |
| Infrastructure | Docker Compose, Kafka UI |

## Lancer le projet

Prérequis : **Java 21** ou plus, Docker.

### 1. Démarrer Kafka avec Docker Compose

Le fichier [`docker-compose.yml`](docker-compose.yml) lance un broker Kafka prêt à l'emploi et une interface web pour l'observer :

```bash
git clone https://github.com/erryhany/kafka-spring-cloud-stream.git
cd kafka-spring-cloud-stream
docker compose up -d
```

| Service | Adresse |
|---|---|
| Kafka (broker) | `localhost:9092` |
| Kafka UI (topics et messages) | http://localhost:8090 |

### 2. Démarrer l'application

```bash
./mvnw spring-boot:run        # Windows : mvnw.cmd spring-boot:run
```

Puis ouvrir **http://localhost:8080** : le graphique affiche en continu le nombre de visites des pages P1 et P2 sur les 5 dernières secondes. Dans Kafka UI, les topics `T2`, `T3` et `T4` se remplissent en temps réel.

Si le port 8080 est déjà pris : `./mvnw spring-boot:run -Dspring-boot.run.arguments=--server.port=8081`.

Arrêt de Kafka : `docker compose down`.

## Endpoints

| Méthode | Route | Description |
|---|---|---|
| GET | `/publish?name=P1&topic=T2` | Publie un événement de page sur le topic indiqué et le renvoie |
| GET | `/analytics` | Flux SSE des comptages par page (fenêtre de 5 s), envoyé chaque seconde |
| GET | `/` | Tableau de bord temps réel (`index.html`) |

## Topics Kafka

| Topic | Producteur | Consommateur |
|---|---|---|
| `T2` | `/publish` | `pageEventConsumer` |
| `T3` | `pageEventSupplier` | `KStreamFunction` |
| `T4` | `KStreamFunction` | aucun (résultats agrégés) |

## Pistes d'évolution

- Tests d'intégration avec le Test Binder et Testcontainers
- Gestion des erreurs et dead letter topic
- Topics aux noms explicites (`page-events`, `page-analytics`…)
- Dockerfile pour l'application

## Auteur

**Mourad Erryhany** — Développeur Java / Spring Boot · [GitHub](https://github.com/erryhany)
