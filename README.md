# web-service-gin

This is a simple API built using Go and the Gin web framework. This is the result of [this](https://go.dev/doc/tutorial/web-service-gin) tutorial created by the Go team.

There is only one difference between the original code from the tutorial and the code in this repo. The `postAlbums` function. See below.

Original:
```go
func postAlbums(c *gin.Context) {
    var newAlbum album

    // Call BindJSON to bind the received JSON to
    // newAlbum.
    if err := c.BindJSON(&newAlbum); err != nil {
        return
    }

    // Add the new album to the slice.
    albums = append(albums, newAlbum)
    c.IndentedJSON(http.StatusCreated, newAlbum)
}
```

Modified:
```go
func postAlbums(c *gin.Context) {
	var newAlbums []album

	// Call BindJSON to bind the received JSON to
	// newAlbum.
	if err := c.BindJSON(&newAlbums); err != nil {
		return
	}

	// Add each album the new newAlbums to the slice.
	for _, newAlbum := range newAlbums {
		albums = append(albums, newAlbum)
	}
	c.IndentedJSON(http.StatusCreated, newAlbums)
}
```

This change was implemented in order to allow posting more than one item per API call. The original function will not handle two or more items.