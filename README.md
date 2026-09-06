# About
dbt (data-build-tool) takes care of the transformation portion of the ELT process. This repo was created to get familiar 
with the basics, and be able to have a quick POC available in a few minutes. The chosen database in this case is postgres
and is it managed through docker.

# Setup
## Requirements
- python 3.11  
- git  
- docker

## Installation
1. Clone the repo
```
git clone https://github.com/rteruyas/dbt_postgres.git  
cd dbt_postgres
```
2. Create virtual environment 
```
python -m venv dbt-env
dbt-env\Scripts\activate         # windows 
#source dbt-env/bin/activate     # linux  
```
3. Install dependencies
```
python -m pip install --upgrade pip
pip install -r requirements.txt
```
4. postgres : docker-compose.yaml   
Postgres database will be dockerized.  
The file *docker-compose.yml* has all the information needed for this project.
```
services:
  postgres:
    image: postgres:16
    container_name: dbt-postgres
    env_file: .env
    ports:
      - "5432:5432"
    volumes:
      - dbt-postgres-data:/var/lib/postgresql/data

volumes:
  dbt-postgres-data:
```
5. Modify .env.example (committed) and .env (not committed)
Make a copy of .env.example and name it .env  
This file will store all your credentials to connect to postgres db
Edit it if you want other values
```
POSTGRES_USER=USER_NAME
POSTGRES_PASSWORD=PASSWORD_VALUE
POSTGRES_DB=DB_NAME
```
6. Start the database
```
docker compose up -d
```
7. Start the project  
This was already started (there is already a folder my_project)
```
dbt init my_project
```
8. Check connection
```
cd my_project
dbt debug
```
9. Make sure it actually runs
```
dbt run
``` 
It is fine if there is nothing to build yet. It should report zero models.  
There are two models included under /my_project/models/example. These are to be deleted once you have your own models.

