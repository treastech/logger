# logger [![GoDoc][doc-img]][doc] [![Go Report Card](https://goreportcard.com/badge/github.com/Treastech/logger)](https://goreportcard.com/report/github.com/Treastech/logger)
Simple go-chi logging middleware for zap 

## Installation
```bash
go get github.com/Treastech/logger
```

## Usage
```go
package main

import (
	l "github.com/Treastech/logger"
	"github.com/go-chi/chi"
	"go.uber.org/zap"
	"net/http"
)

func main() {

	logger, _ := zap.NewProduction()
	defer logger.Sync() // flushes buffer, if any

	r := chi.NewRouter()

	// instead of
	// r.Use(middleware.Logger)
	// use
	r.Use(l.Logger(logger))
	r.Get("/", func(w http.ResponseWriter, r *http.Request) {
		w.Write([]byte("welcome"))
	})
	http.ListenAndServe(":3000", r)
}
```

## Sample log output
```
{"level":"info","ts":1530826215.6541932, "msg":"Served","proto":"HTTP/1.1","path":"/","lat":0.032019407,"status":200,"size":7,"reqId":"localhost/FsNkQGYAQA-000036"}
```


[doc-img]: https://godoc.org/github.com/Treastech/logger?status.svg
[doc]: https://godoc.org/github.com/Treastech/logger
