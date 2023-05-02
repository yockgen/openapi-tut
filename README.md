# Golang Restful and OpenAPI tutorial

### Run Gin Example
```
root@KBL02:/data/openapi# cd ./web-service-gin/
root@KBL02:/data/openapi/web-service-gin# go run .
[GIN-debug] [WARNING] Creating an Engine instance with the Logger and Recovery middleware already attached.

[GIN-debug] [WARNING] Running in "debug" mode. Switch to "release" mode in production.
 - using env:   export GIN_MODE=release
 - using code:  gin.SetMode(gin.ReleaseMode)

[GIN-debug] GET    /albums                   --> main.getAlbums (3 handlers)
[GIN-debug] POST   /albums                   --> main.postAlbums (3 handlers)
[GIN-debug] GET    /albums/:id               --> main.getAlbumByID (3 handlers)
[GIN-debug] GET    /albums/:id/:sales        --> main.getMultiParams (3 handlers)
[GIN-debug] [WARNING] You trusted all proxies, this is NOT safe. We recommend you to set a value.
Please check https://pkg.go.dev/github.com/gin-gonic/gin#readme-don-t-trust-all-proxies for details.
[GIN-debug] Listening and serving HTTP on localhost:8080

```

### Test with CURL
```
root@KBL02:~# curl http://localhost:8080/albums
[
    {
        "id": "1",
        "title": "Blue Train",
        "artist": "John Coltrane",
        "price": 56.99,
        "sales": 0
    },
    {
        "id": "2",
        "title": "Jeru",
        "artist": "Gerry Mulligan",
        "price": 17.99,
        "sales": 0
    },
    {
        "id": "3",
        "title": "Sarah Vaughan and Clifford Brown",
        "artist": "Sarah Vaughan",
        "price": 39.99,
        "sales": 0
    }
]
```
```
root@KBL02:~# curl http://localhost:8080/albums/1/666
{
    "id": "1",
    "title": "Blue Train",
    "artist": "John Coltrane",
    "price": 56.99,
    "sales": 666
}
```

```
root@KBL02:~# curl http://localhost:8080/albums \
>     --include \
>     --header "Content-Type: application/json" \
>     --request "POST" \
>     --data '{"id": "4","title": "The Modern Sound of Betty Carter","artist": "Betty Carter","price": 49.99}'
HTTP/1.1 201 Created
Content-Type: application/json; charset=utf-8
Date: Tue, 02 May 2023 04:46:47 GMT
Content-Length: 132

{
    "id": "4",
    "title": "The Modern Sound of Betty Carter",
    "artist": "Betty Carter",
    "price": 49.99,
    "sales": 0
}
```
