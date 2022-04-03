# Network Programming with Go

## 8. Writing HTTP Clients

### Understanding the Basics of HTTP

- HTTP is a sessionless client-server protocol in which the client initiates a request to the server and the server responds to the client.
- HTTP is an `application layer` protocol. Uses `TCP` as its underlying transport layer protocol.

#### Uniform Resource Locators

> scheme://user:password@host:port/path?key1=value1&key2=value2#table_of_contents

- query string, parameters
  > https://www.google.com/search?q=gophers&tbm=isch

#### Client Resource Requests

- request = method + target resource + headers + body

#### Server Responses

- 200-class : successful request
- 300-class : further action on the client's part needed
- 400-class : error on the client's request
- 500-class : error on the server side

### Retrieving Web Resources in Go

#### Methods

- `GET`, `HEAD`, `POST`, `PUT`, `DELETE` : mostly used
  - `HEAD` : request ONLY the head, NOT payload
    - USEFUL whether a resource EXISTS
    - USEFUL inspecting response headers BEFORE retrieving the resource

#### Time-outs

- `context`'s timer starts running as soon as you initialize the context.

#### Disabling Persistent TCP Connections

- Inform the client what to do with the TCP socket on a `per-request` basis

  ```go
  // --snip--
  req, err := http.NewRequestWithContext(ctx, http.MethodGet, ts.URL, nil)
  if err != nil {
  t.Fatal(err)
  }
  req.Close = true
  // --snip--

  ```

### Posting Data over HTTP

#### Posting JSON to a Web Server

- need to create a handler that can accept data

#### Posting a Multipart Form with Attached Files

- use `mime/multipart` package
  > Multipurpose Internet Mail Extensions (MIME) messages : support the transfer of single or multiple text and non-text attachments(graphics, audio video files)
- `go test -v` : shows output

### What You've Learned

#### Close the Response Body

#### No Time out : `http.Get`, `http.Head`, `http.Post` (feat. Context)
