1. How many artists are in the database?

    Query :-
    ```
    query {
    artist_aggregate {
        aggregate {
        count
        }
    }
    }
    ```

    Output :- 
    ```
    {
    "data": {
        "artist_aggregate": {
        "aggregate": {
            "count": 275
        }
        }
    }
    }
    ```

2.  List the first track of every album by every artist in ascending order.

    Pre : Relationship created between artist, album and track table to perform this operation 

    Query :-
    ```
    query GetFirstTrackOfAlbums {
    artist(order_by: { name: asc }) {
        name
        artist_albums(order_by: { title: asc }) {
        title
        album_tracks(limit: 1, order_by: { name: asc }) {
            name
        }
        }
    }
    }
    ```

    Output is stored in below path due to long output:- 
    ```
    File : task-one-output/Q2-output.json
    ```

3. Get all albums for artist id = 5 without specifying a where clause.

    Pre : 

    1. Create a role name "artist" with permission "X-Hasura-Artist-Id" for row. Also allowed column "title" and "album_id" for the same. 

    2.  Header used 
    ```
    X-Hasura-Artist-Id = 5
    x-hasura-role = artist
    ```

    Query :-
    ```
    query GetAlbums {
    album {
        album_id
        title
    }
    }
    ```

    Output :- 
    ```
    {
    "data": {
        "album": [
        {
            "album_id": 7,
            "title": "Facelift"
        }
        ]
    }
    }
    ```

4. Using a GraphQL mutation, add your favorite artist and one of their albums that isn’t in
the dataset.


    1. Created artist with name "Qamar Hashmi" and Id = 346 with admin permission 

    Query :-
    ```
    mutation AddArtist {
    insert_artist_one(object: { name: "Qamar Hashmi",artist_id:346 }) {
        artist_id
        name
    }
    }
    ```

    Output : 

    ```
    {
    "data": {
        "insert_artist_one": {
        "artist_id": 346,
        "name": "Qamar Hashmi"
        }
    }
    }
    ```

    2. Created album with for artist_id = 346 with admin permission 

    Query :-
    ```
    mutation AddAlbum {
    insert_album_one(object: {album_id: 348, artist_id: 346, title: "My title Song"}) {
        album_id
        artist_id
        title
    }
    }
    ```

    Output : 
    ```
    {
    "data": {
        "insert_album_one": {
        "album_id": 348,
        "artist_id": 346,
        "title": "My title Song"
        }
    }
    }
    ```

5. How did you identify which ID to include in the mutation?

    1. I followed 2 approaches, first, maunally checked the table last entry(to add new/next ID) to find out artist_id.
  
   Query :-
    ```
    mutation AddAlbum {
    insert_album_one(object: {album_id: 348, artist_id: 346, title: "My title Song"}) {
        album_id
        artist_id
        title
    }
    }
    ```
    2. Second, I went ahead and updated the "artist_id" to auto-generate the sequence as it is a primary key using following SQL command

    Query :- 
    ```
    CREATE SEQUENCE artist_id_seq START 348;
    ALTER TABLE artist ALTER COLUMN artist_id SET DEFAULT nextval('artist_id_seq');
    ----------
    mutation AddArtist {
    insert_artist_one(object: { name: "my-artist" }) {
        artist_id  # it auto-generates the artist_id by the database 
        name
    }
    }
    ```

