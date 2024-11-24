1. Share your query, the headers used and the results of the following three queries:

    For Query 1 : 
    
    a. First, I created a relationship between table track and genre with name "track_genre" 
    
    b. In the given query, table name was mentioned as "Tracks". Looking at the database, I found the table name was "track" so updated the same. 
    
    c. Last, under where clause it was mentioned "genre", I updated to "track_genre" i.e., the name created for relationship

    Query : 
    ```
    query getTracks($genre: String, $limit: Int, $offset: Int) {
    track(limit: $limit, offset: $offset, where: {track_genre: {name: {_eq: $genre}}}) {
        name
        track_id
    }
    }
    ```
    Output : 

    ```
    {
    "data": {
        "track": [
        {
            "name": "Trupets Of Jericho",
            "track_id": 190
        },
        {
            "name": "Machine Men",
            "track_id": 191
        },
        {
            "name": "The Alchemist",
            "track_id": 192
        },
        {
            "name": "Realword",
            "track_id": 193
        },
        {
            "name": "Free Speech For The Dumb",
            "track_id": 408
        }
        ]
    }
    }
    ```

    For Query 2 : 

    a. First created a role named "artist" with below check
        {"artist_id":{"_eq":"x-hasura-artist-id"}}
        and column permission "title" and "album_id"

    b. While doing query, we passed below headers 
        x-hasura-role = artist
        x-hasura-artist-id = 1 #Random
    
    c. In the query, "album" was spelled as "albums". Therefore, modified it to "album" to fix the query issue. 
    
    Query : 

    ```
    query getAlbumsAsArtist {
    album {
        title
    }
    }
    ```

    Output : 

    ```
    {
    "data": {
        "album": [
        {
            "title": "For Those About To Rock We Salute You"
        },
        {
            "title": "Let There Be Rock"
        }
        ]
    }
    }
    ```


    For Query 3 : 

    a. First created a relationship between table "track" and "album" for mapping "artist_id" with header ID
    
    b. Created a "artist" role in track table with below check
    {"track_album":{"artist_id":{"_eq":"x-hasura-artist-id"}}}

    b. Added column permission for "unit_price"

    d. Also enabled Aggregate permssion as it throwing error for "track_aggregate" permission.

    e. Used same header as of query 2 

    Query :

    ```
    query trackValue {
    track_aggregate {
        aggregate {
        sum {
            unit_price
        }
        }
    }
    }
    ```

    Output : 

    ```
    {
    "data": {
        "track_aggregate": {
        "aggregate": {
            "sum": {
            "unit_price": 17.82
            }
        }
        }
    }
    }
    ```


2. Execute a complex query of your choice, with and without caching. Share the query, the
response and the response time for each.


    a. Used "admin" role for this operation
    b. Used header "cache-control" for caching query 

    ```
    query complexQuery {
    album(where: {album_tracks: {track_genre: {name: {_eq: "Metal"}}}}) {
        title
        album_tracks {
        name
        }
    }
    }
    ```

    > Without Cache
    ```
    Response Time 27 ms 
    Response Size 26910 bytes
    ```

    > With Cache

    ```
    Response Time 22 ms
    Response Size 26910 bytes
    ```
