>>> Task one steps performed to achieve Task 1: 

1. Installed Docker Desktop on my machine

2. I was unable to find the init.sql on the repository so used the same one(task one) Chinook_PostgreSql.sql file for the PostgreSQL database. 
   
   Download link : https://github.com/lerocha/chinook-database/releases

3. Created a directory for task1 with name “hasura-task-two”.

4. Created a docker-compose.yaml file in the root of the directory “hasura-task-one”.
          
    Image used from docker hub :- 
    a. postgres image = postgres:15 and 
    b. graphql-engine = hasura/graphql-engine:v2.25.0 # As image "hasura/graphql-engine:v2.48.2-pro" is not a public image

5. Created the containers using command "docker-compose up -d" and ensured docker containers are running using command "docker ps". Below is the output :
    ----------------------------
    mdqamarhashmi@Mds-MacBook-Air hasura-task-two % docker ps
    CONTAINER ID   IMAGE                           COMMAND                  CREATED        STATUS                 PORTS                    NAMES
    82f6f34fc1a0   hasura/graphql-engine:v2.25.0   "graphql-engine serve"   2 hours ago    Up 2 hours (healthy)   0.0.0.0:8080->8080/tcp   hasura-graphql
    5f279de61395   redis:latest                    "docker-entrypoint.s…"   18 hours ago   Up 2 hours             0.0.0.0:6379->6379/tcp   hasura-task-two-redis-1
    efc429e775f7   postgres:15                     "docker-entrypoint.s…"   18 hours ago   Up 2 hours             0.0.0.0:5432->5432/tcp   hasura-task-two-postgres-1
    ----------------------------

6. Copied the "Chinook_PostgreSql.sql" to container "chinook-postgres".
    ----------------------------
    docker cp Chinook_PostgreSql.sql efc429e775f7:/
    Successfully copied 602kB to efc429e775f7:/Chinook_PostgreSql.sql
    ----------------------------

7. Loaded up the Chinook_PostgreSql.sql in PostgreSql container
    ----------------------------
    psql -U postgres -d chinook -f Chinook_PostgreSql.sql
    psql:Chinook_PostgreSql.sql:19: ERROR:  cannot drop the currently open database
    psql:Chinook_PostgreSql.sql:25: ERROR:  database "chinook" already exists
    You are now connected to database "chinook" as user "postgres".
    CREATE TABLE
    CREATE TABLE
    CREATE TABLE
    :
    :
    INSERT 0 1000
    INSERT 0 1000
    INSERT 0 1000
    INSERT 0 715
    ----------------------------

8. Once the database was up and running, I accessed the application on http:localhost:8080/console and started performing steps executing mentioned the pdf. Please refer "graphql-queries-&-output.md" file under "hasura-task-two" folder for more details. 




>>> Challenges and Troubleshooting : 

1. Firstly, the challenge was image reference given in docker-compose.yaml was a private image. Therefore, I searched for public image available on docker hub and I was able to use them. 

