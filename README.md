# Installer-PostgreSQL-et-PgAdmin-via-Docker-




# 🚀 Installer PostgreSQL et PgAdmin via Docker

**Auteur :** Christian TOUGNIA  
**Date :** 26 avril 2025  

---

##  Introduction

Salut ! Dans ce petit guide, je vais t’expliquer comment installer **PostgreSQL** et **PgAdmin** avec **Docker** en quelques étapes simples et rapides.  
L’objectif : t’offrir un environnement facile à déployer, reproductible, et sans prise de tête ! 😎

---

##  Pourquoi utiliser PostgreSQL et PgAdmin ?

### 🐘 PostgreSQL — La star des bases de données

PostgreSQL est une base de données **open source**, robuste et ultra-puissante.  
Elle supporte :

- les **requêtes SQL complexes**
- le **JSON**
- la **géolocalisation**
- et bien plus encore !

Utilisé par de nombreuses entreprises pour leurs applications critiques, PostgreSQL est un pilier du développement moderne.

###  PgAdmin — Ton assistant graphique

PgAdmin est une **interface web** pour administrer PostgreSQL facilement.  
Tu peux :

- exécuter des requêtes SQL
- importer/exporter des données
- créer des sauvegardes
- explorer ta base via une interface intuitive

---

## 🛠️ Installation avec Docker

> ⚠️ Assure-toi d’avoir [Docker installé](https://www.docker.com/products/docker-desktop) sur ta machine avant de commencer.

---

### ✅ Étape 1 : Récupérer l’image PostgreSQL

```bash
docker pull postgres:16.2
```

### ✅ Étape 2 : Lancer un conteneur PostgreSQL 

```bash
docker run --name pgserver-local \
  -e POSTGRES_PASSWORD=MonMotDePasse \
  -p 5432:5432 \
  -d postgres:16.2
```
🔑 Remplace MonMotDePasse par un mot de passe sécurisé de ton choix.
Ce conteneur héberge ton serveur PostgreSQL.


### ✅ Étape 3 : Récupérer l’image PgAdmin

```bash
docker pull dpage/pgadmin4:8.4
```

Cette commande télécharge la version 8.4 de PgAdmin depuis Docker Hub.

### ✅  Étape 4 : Lancer un conteneur PgAdmin

```bash
docker run --name pgadmin \
  -e PGADMIN_DEFAULT_EMAIL=ton.email@exemple.com \
  -e PGADMIN_DEFAULT_PASSWORD=Secret123 \
  -p 5050:80 \
  -d dpage/pgadmin4:8.4
```
🔑 Remplace ton.email@exemple.com et Secret123 par tes identifiants personnels.

### ✅ Étape 5 : Créer un réseau Docker pour connecter PostgreSQL et PgAdmin 

Créer un réseau Docker :

```bash
docker network create postgres-network
```

Connecter les conteneurs au réseau :

```bash
docker network connect postgres-network pgserver-local
docker network connect postgres-network pgadmin
```
💡 Ce réseau permet à PgAdmin de communiquer avec le serveur PostgreSQL sans configuration complexe.

###  ✅ Étape 6 : Vérifier les IPs des conteneurs

```bash
docker inspect pgserver-local
docker inspect pgadmin
```

### 🖥️ Accéder à PgAdmin

Ouvre ton navigateur à l’adresse : http://localhost:5050
Connecte-toi avec l’e-mail et le mot de passe définis à l’étape 4
Dans PgAdmin, crée un nouveau Server :
Name : ce que tu veux (ex. : PostgresLocal)
Host name/address : pgserver-local
Port : 5432
Username : postgres
Password : celui de l’étape 2



### 🎉 Conclusion

Avec Docker, tu viens de mettre en place un environnement complet de base de données :

✅ PostgreSQL — Puissant et fiable
✅ PgAdmin — Facile à utiliser, parfait pour les débutants
✅ Docker — Déploiement simple, rapide et propre

⭐ N’hésite pas à laisser une étoile sur ce dépôt si ce tutoriel t’a été utile !
