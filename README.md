# Usage

```go
package main

import (
	"time"

	"github.com/BiteBit/ginlog"
	"github.com/gin-gonic/gin"
)

func main() {
	router := gin.New()

	router.Use(Logger())

	router.GET("/", func(c *gin.Context) {
		c.JSON(200, "Hello world!")
	})

	router.Run(":8080")
}

func Logger() gin.HandlerFunc {
	logger, err := ginlog.NewProductionLogger()
	if err != nil {
		panic(err)
	}

	return ginlog.Logger(logger, ginlog.Options{
		TimeFormat:        time.RFC3339,
		RequestBodyLimit:  2000,
		RequestQueryLimit: 2000,
		ResponseBodyLimit: 2000,
	})
}
```