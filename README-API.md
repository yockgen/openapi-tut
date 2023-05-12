## Telemetry Manager Open API

<table> 
  <tr>
     <th>API</th><th>Description</th><th>Result</th><th>Payload</th>
  </tr> 
  <tr valign="top">
    <td> /telegraf/schema </td>    
    <td> 
     return available buckets
     </td>
     <td>
        <code>
         [
           {
                "id": "1",
                "type": "bucket",
                "name": "Intel"                        
            }
            ...
          ]
        </code> 
     </td>  
     <td>&nbsp;</td>     
  </tr>
 
 <tr valign="top">
    <td> /telegraf/metrices </td>    
    <td> 
     return available metrices
     </td>
     <td>
        <code>
         [
           {
                "id": "1",
                "type": "metric",
                "name": "cpu_usage"        
                 "bucket": "Intel"
            },         
           {
                "id": "2",
                "type": "metric",
                "name": "mem_usage"        
                 "bucket": "Intel"
            },         
            {
                "id": "3",
                "type": "metric",
                "name": "gpu_usage"        
                 "bucket": "Intel"
            }         
            ...
          ]
        </code> 
     </td>  
     <td>&nbsp;</td>
  </tr>
 
 <tr valign="top">
    <td> /telegraf/metrices/:id/:start/:end </td>    
    <td> 
     return selected metric metric rows with specific period
     </td>
     <td>
        <code>
         [
           {
                "id": "1",                
                "value": "80"        
                "timestamp": "2023-05-21 17:00:00.000"
            },         
            {
                "id": "2",                
                "value": "70"        
                "timestamp": "2023-05-21 16:00:00.000"
            },                    
            ...
          ]
        </code> 
     </td>  
     <td>
     </td>
     
  </tr>
 
</table>

# Golang Restful and OpenAPI tutorial

### Run Gin Example
```
$ cd ./web-service-gin/
$ go run .
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
$ curl http://localhost:8080/albums
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
$ curl http://localhost:8080/albums/1/666
{
    "id": "1",
    "title": "Blue Train",
    "artist": "John Coltrane",
    "price": 56.99,
    "sales": 666
}
```

```
$ curl http://localhost:8080/albums \
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
