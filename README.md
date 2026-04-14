---

# 🧠 Neo4j Basketball Graph Database

This project demonstrates how to use **Neo4j (Graph Database)** with **Cypher queries** to model and analyze basketball data such as players, teams, coaches, and game statistics.

---

## 📌 Project Overview

This dataset represents:

* 🏀 Players (with attributes like height, weight, age)
* 🏆 Teams
* 🎯 Coaches
* 🔗 Relationships:

  * `PLAYS_FOR`
  * `TEAMMATES`
  * `COACHES`
  * `COACHES_FOR`
  * `PLAYED_AGAINST`

---

## 🛠️ Tech Stack

* Neo4j Graph Database
* Cypher Query Language

---

## 📂 Project Structure

```
.
├── query.cypher              # Basic CRUD & query operations
├── 01-initial-data.cypher    # Initial dataset (nodes + relationships)
└── README.md
```

---

## 🚀 Getting Started

### 1. Install Neo4j

* Download Neo4j Desktop or use Neo4j Aura (cloud)
* Start a database

---

### 2. Load Initial Data

Run:

```cypher
:play 01-initial-data.cypher
```

OR paste contents manually into Neo4j Browser.

---

### 3. Run Queries

Execute queries from:

```cypher
query.cypher
```

---

## 📊 Data Model

### 🧍 PLAYER

Properties:

* `name`
* `age`
* `number`
* `height`
* `weight`

### 🏀 TEAM

* `name`

### 🎯 COACH

* `name`

---

## 🔗 Relationships

| Relationship     | Description                        |
| ---------------- | ---------------------------------- |
| `PLAYS_FOR`      | Player belongs to a team           |
| `TEAMMATES`      | Player-to-player connection        |
| `COACHES`        | Coach trains players               |
| `COACHES_FOR`    | Coach manages a team               |
| `PLAYED_AGAINST` | Game stats between player and team |

---

## 📘 Query Examples

### 🔍 Basic Queries

```cypher
// Get all players
MATCH (p:PLAYER) RETURN p;

// Find player by name
MATCH (p:PLAYER {name: "LeBron James"}) RETURN p;
```

---

### 📏 Filtering

```cypher
// Players taller than 2 meters
MATCH (p:PLAYER)
WHERE p.height >= 2
RETURN p;
```

---

### ⚖️ BMI Calculation

```cypher
MATCH (p:PLAYER)
WHERE (p.weight / (p.height * p.height)) > 25
RETURN p;
```

---

### 🔗 Relationship Queries

```cypher
// Players in LA Lakers
MATCH (p:PLAYER)-[:PLAYS_FOR]->(t:TEAM)
WHERE t.name = "LA Lakers"
RETURN p, t;
```

---

### 💰 Salary-Based Query

```cypher
MATCH (p:PLAYER)-[c:PLAYS_FOR]->(t:TEAM)
WHERE c.salary >= 40000000
RETURN p, t, c;
```

---

### 🤝 Teammates

```cypher
MATCH (p:PLAYER {name: "LeBron James"})-[:TEAMMATES]-(mate:PLAYER)
RETURN mate;
```

---

### 📊 Aggregations

```cypher
// Total games played
MATCH (p:PLAYER)-[g:PLAYED_AGAINST]->(:TEAM)
RETURN p.name, COUNT(g) AS games
ORDER BY games DESC;
```

```cypher
// Total minutes played
MATCH (p:PLAYER)-[g:PLAYED_AGAINST]->(:TEAM)
RETURN p.name, SUM(g.minutes) AS minutes
ORDER BY minutes DESC;
```

```cypher
// Average points
MATCH (p:PLAYER)-[g:PLAYED_AGAINST]->(:TEAM)
RETURN p.name, AVG(g.points) AS avg_points
ORDER BY avg_points DESC;
```

---

## ✏️ CRUD Operations

### ✅ Create Node

```cypher
CREATE (p:PLAYER {name: "LeBron James", height: 2.01})
RETURN p;
```

---

### 🔄 Update Node

```cypher
MATCH (p:PLAYER {name: "LeBron James"})
SET p.age = 36
RETURN p;
```

---

### 🏷️ Add Label

```cypher
MATCH (p:PLAYER {name: "LeBron James"})
SET p:REF
RETURN p;
```

---

### ❌ Remove Property

```cypher
MATCH (p:PLAYER {name: "LeBron James"})
REMOVE p.age
RETURN p;
```

---

### ❌ Delete Node

```cypher
MATCH (p {name: "Ja Morant"})
DETACH DELETE p;
```

---

### ❌ Delete Relationship

```cypher
MATCH (p)-[r:PLAYS_FOR]->()
DELETE r;
```

---

### ⚠️ Delete Entire Database

```cypher
MATCH (n)
DETACH DELETE n;
```

---


---

## 🎯 Use Cases

* Sports analytics
* Relationship-based queries
* Graph learning (Neo4j beginners)
* Data visualization in graph form

---

## 📈 Key Learnings

* Graph databases are powerful for **connected data**
* Cypher is intuitive for **relationship traversal**
* Aggregations + relationships = strong insights

---

## 🧑‍💻 Author

**Mohamed Jamaludeen**

* MCA Graduate
* Backend Developer (Python  / APIs)
* Exploring Graph Databases & System Design

---

## ⭐ Future Improvements

* Add indexes for performance
* Use Neo4j Bloom for visualization
* Build REST API using Flask/FastAPI
* Add authentication layer

---


