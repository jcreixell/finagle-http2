# Enabling HTTP/2 in Finagle

Example of enabling HTTP/2 in Finagle via [toggle](https://github.com/jcreixell/finagle-http2/blob/master/src/main/resources/com/twitter/toggles/configs/com.twitter.finagle.http-service.json).

## Usage

### Server

Run the server with:

```bash
$ sbt "runMain com.jcreixell.finaglehttp2.Server"
```

Test it with `curl` (make sure it is compiled with support for [nghttp2](https://curl.haxx.se/docs/http2.html)):

```bash
$ curl --http2 -v localhost:8080
```

### Client

Run the client with:

```scala
$ sbt "runMain com.jcreixell.finaglehttp2.Client"
```

To test it, you can use [netcat](http://netcat.sourceforge.net/). Before running the client:

```bash
nc -l -p 8080
```

You should see the upgrade headers:

```
upgrade: h2c
HTTP2-Settings: AAEAABAAAAIAAAABAAN_____AAQAAP__AAUAAEAAAAYAACAA
connection: HTTP2-Settings,upgrade
```

## Benchmarking

For benchmarking, you can use h2load (part of [nghttp2](https://nghttp2.org/)):

For HTTP/1.1:

```bash
h2load --h1 -n100000 -c100 -m10 http://localhost:8080
```

For HTTP/2:

```bash
h2load -n100000 -c100 -m10 http://localhost:8080
```
