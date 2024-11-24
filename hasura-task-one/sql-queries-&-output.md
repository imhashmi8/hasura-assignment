1. Return the artist with the most number of albums

    Query : 
    ```
    SELECT artist.name, COUNT(album.album_id) AS album_count
    FROM artist
    JOIN album ON artist.artist_id = album.artist_id
    GROUP BY artist.artist_id
    ORDER BY album_count DESC
    LIMIT 1;
    ```
    
    Output : 
    ```

        name     | album_count 
    -------------+-------------
    Iron Maiden |          21
    (1 row)
    ```


2. Return the top three genres found in the dataset in descending order

    Query : 
    ```
    SELECT g.name AS genre, COUNT(t.track_id) AS track_count
    FROM track t
    JOIN genre g ON t.genre_id = g.genre_id
    GROUP BY g.name
    ORDER BY track_count DESC
    LIMIT 3;
    ```

    Output : 
    ```
    genre | track_count 
    -------+-------------
    Rock  |        1297
    Latin |         579
    Metal |         374
    (3 rows)
    ```

3. Return the number of tracks and average run time for each media type

    Query :- 
    ```
    SELECT mt.name AS media_type, 
       COUNT(t.track_id) AS track_count, 
       AVG(t.milliseconds / 1000.0) AS avg_run_time_seconds
    FROM track t
    JOIN media_type mt ON t.media_type_id = mt.media_type_id
    GROUP BY mt.name
    ORDER BY track_count DESC;
    ```

    Output :- 
    ```

             media_type          | track_count | avg_run_time_seconds  
    -----------------------------+-------------+-----------------------
    MPEG audio file             |        3034 |  265.5742887277521424
    Protected AAC audio file    |         237 |  281.7238734177215190
    Protected MPEG-4 video file |         214 | 2342.9404252336448598
    AAC audio file              |          11 |  276.5069090909090909
    Purchased AAC audio file    |           7 |  260.8947142857142857
    (5 rows)
   ```
