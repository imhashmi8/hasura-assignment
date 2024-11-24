Task one steps performed to achieve Task 1: 

1. Installed Docker Desktop on my machine

2. Downloaded the Chinook_PostgreSql.sql file for the PostgreSQL database. 
   ```
   Download link : https://github.com/lerocha/chinook-database/releases
   ```

3. Created a directory for task1 with name “hasura-task-one”.

4. Created a docker-compose.yaml file in the root of the directory “hasura-task-one”.
   ```     
    Image used from docker hub :- 
    a. postgres image = postgres:13 and 
    b. graphql-engine = hasura/graphql-engine:v2.25.0
   ```

5. Created the containers using command "docker-compose up -d" and ensured docker containers are running using command "docker ps". Below is the output :
    ```
    mdqamarhashmi@Mds-MacBook-Air hasura-task-one % docker ps
    CONTAINER ID   IMAGE                           COMMAND                   CREATED          STATUS                    PORTS                    NAMES
    5566c493fc00   hasura/graphql-engine:v2.25.0   "/bin/sh -c '\"${HGE_…"   40 seconds ago   Up 40 seconds (healthy)   0.0.0.0:8080->8080/tcp   hasura-graphql
    e610e32072d0   postgres:13                     "docker-entrypoint.s…"    3 hours ago      Up 3 hours (healthy)      0.0.0.0:5432->5432/tcp   chinook-postgres
    ```

6. Copied the "Chinook_PostgreSql.sql" to container "chinook-postgres".
    ```
    docker cp Chinook_PostgreSql.sql e610e32072d0:/
    Successfully copied 602kB to e610e32072d0:/Chinook_PostgreSql.sql
    ```

7. Loaded up the Chinook_PostgreSql.sql in PostgreSql container
    ```
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
    ```

8. Once the database was up and running, I accessed the application on http:localhost:8080/console and started performing steps executing mentioned the pdf. Please refer file 

"graphql-queires-&-output.md" and "sql-queries-&-output.md" for GraphQL API queries/output and SQL statement queries/output respectively. 


>>> Challenges and Troubleshooting : 

1. Firstly the challenge was no docker-compose.yaml available for task-1. However, I was able to create a one using the reference from the docker-compose.yaml given in Task 2. 

2. Second challenge was image reference given in docker-compose.yaml was a private image. Therefore, I searched for public image available on docker hub and I was able to use them. 

3. After setting up docker-compose.yaml, I faced few other problems like container continously getting restarted. Upon inspecting the logs of the contianers. I was slowly progressing and successfully able to make both the containers running. 

4. Although both containers was running, I was still not able to access the application. Upon carefully reviewing the docker-compose.yaml file given for task-2, I noticed environment variable like HASURA_GRAPHQL_ENABLE_CONSOLE and HASURA_GRAPHQL_DEV_MODE is not set to true. Upon setting it to true. I was successfully able to access the application on "http:localhost:8080/console". 

5. Next, I browser the console properly to understand the options available and how to use it. Later, I checked few demo vidoes/docs on youtube/google to understand graphql syntax and it's working. 

Note : This was the first time, I was working with graphql so it took me some time to understand the requirement and frame query. Gradually, I started understanding the syntax and I was able to frame queries. 

6. I also faced some issues while making queries but console error highliter feature was helpfull. Based on error, I was able to research and fix the same like permission, creating relationship between the table. 

7. Similarly, I also faced some issues writing SQL queries. However, upon search and deep dive I was able to create queries for the same. 
