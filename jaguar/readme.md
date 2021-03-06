
# jaguar.go

Jaguar is a library to make HTTP requests a little easier in Go. I use it to get
and send requests to API. This replaces a previous [Fetcher][1] library but is
not API compatible hence the new name.

In general, requests aren't too bad using the `net/http` library. However, they
can be even easier, this library is to help with testing a REST API requiring 
setting headers, uploading images and creating more complex requests.

Jaguar is an attempt to clean up how the older library worked, fixes setting
form headers and an overall improved interface. A bit of learning from the
chainable nature of [gorequest][2], however that library does not support file
uploads.


## Install

```
$ go get github.com/automattic/go/jaguar
```


## Usage





### GET Example

Here's a basic GET request example

```go
import "github.com/automattic/go/jaguar"

j := jaguar.New()
j.Url("https://google.com/")
j.Method("GET")
resp, err := j.Send()
if err != nil {
    fmt.Println("Error fetching:", err)
}

fmt.Println("Status Code: ", resp.StatusCode)
```

### Chainable Examples

Most of the methods in Jaguar are chainable, and the Methods are convenience
functions which accept a Url to combine. So the following are all equivalent to
the above example:

```go
j := jaguar.New()
j.Method("GET")
resp, err := j.Url("https://google.com/").Send()
```

```go
j := jaguar.New()
j.Url("https://google.com/")
resp, err := j.Method("GET").Send()
```

```go
j := jaguar.New()
j.Get("https://google.com/")
resp, err := j.Send()
```

```go
j := jaguar.New()
resp, err := j.Get("https://google.com/").Send()
```


### POST Example

Example using POST parameters to a form

```go
j := jaguar.New()
j.Params.Add("q", "golang")
j.Url("https://google.com/")
resp, err := j.Method("POST").Send()
if err != nil {
    fmt.Println("Error Fetching:", err)
}
fmt.Println(resp.String())
```

### File Upload Example

Example uploading a files, setting parameters and header 

```go
j := jaguar.New()
j.Url("/upload-file")
j.Header.Add("X-Auth", "my-secret-token")
j.Params.Add("foo", "bar")
j.Params.Add("baz", "foz")
j.Files["filedata"] = "/home/mkaz/tmp/upload.jpg"
resp, err := j.Method("POST").Send()
if err != nil {
    fmt.Println("Error Fetching:", err)
}
fmt.Println(resp.String())
```

## License

This software is licensed under the MIT License.


[1]: https://github.com/mkaz/fetcher
[2]: https://github.com/parnurzeal/gorequest


