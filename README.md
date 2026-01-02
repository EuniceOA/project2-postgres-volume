# Project 2 — PostgreSQL Database with Docker Volume (Assignment 2)

## Overview
This project demonstrates running a PostgreSQL container with a Docker volume to persist data.

**Requirements completed:**
- Run a PostgreSQL container with a volume
- Create a table and add data
- Delete the container
- Start a new container with the same volume
- Verify the data is still there

---

## Prerequisites
- Docker installed and working
- Linux/Ubuntu terminal

---

## Step-by-step Commands

### 1) Create a Docker volume
```bash
docker volume create pgdata
docker volume ls
2) Run PostgreSQL container with the volume
docker run -d --name postgres-db \
  -e POSTGRES_USER=bootcamp \
  -e POSTGRES_PASSWORD=bootcamp123 \
  -e POSTGRES_DB=assignment2db \
  -p 5432:5432 \
  -v pgdata:/var/lib/postgresql/data \
  postgres:16

docker ps
3) Connect to PostgreSQL
docker exec -it postgres-db psql -U bootcamp -d assignment2db
4) Create table + insert data
Run these inside psql (you should see assignment2db=#):
CREATE TABLE students (
  id SERIAL PRIMARY KEY,
  name TEXT NOT NULL,
  course TEXT NOT NULL
);

INSERT INTO students (name, course) VALUES
('Eunice', 'DevOps Bootcamp'),
('Alex', 'Cloud Computing');

SELECT * FROM students;
exit sql
\q
5) Delete the container
docker stop postgres-db
docker rm postgres-db
docker ps -a
6) Start a NEW container with the SAME volume
docker run -d --name postgres-db \
  -e POSTGRES_USER=bootcamp \
  -e POSTGRES_PASSWORD=bootcamp123 \
  -e POSTGRES_DB=assignment2db \
  -p 5432:5432 \
  -v pgdata:/var/lib/postgresql/data \
  postgres:16

docker ps
7) Verify data is still there
docker exec -it postgres-db psql -U bootcamp -d assignment2db
inside sql:
SELECT * FROM student
exit sql:\q

Author
Eunice Olajumoke
