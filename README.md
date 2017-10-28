# Enabling HTTP/2 in Finagle

Example of enabling HTTP/2 in Finagle via toggle.

## Usage

Run the server with:

```scala
$ sbt run
```

Test it with `curl` (make sure it is compiled with support for [nghttp2](https://curl.haxx.se/docs/http2.html):

```scala
$ curl --http2 -v localhost:8080
```
