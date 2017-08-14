# minihttp

minihttp is a simple and lightweight http client lib for rust.
only provide basic http client feature, more like python request.
minihttp's aim is simple, easy to use, less dependent, smaller binary.
Enjoy your self...

## Online documention

[Document](https://docs.rs/minihttp)

## Usage

###  send a get request

```rust
use minihttp::request::Request;
let mut http = Request::new("http://www.google.com").unwrap();
let res = http.get().send().unwrap();
println!("status code {}",res.status_code());
println!("reason {}",res.reason());
println!("body {}",res.text());
for (k,v) in res.headers(){
​     println!("{}:{}",k,v);
}
```

### send a post request

```rust
use minihttp::request::Request;

let mut http = Request::new("http://www.google.com").unwrap();
let res = http.post().body_str("hello").send().unwrap();
println!("status code {}",res.status_code());
```

### custom headers
```rust
use std::collections::HashMap;
use minihttp::request::Request;

let mut http = Request::new("http://www.google.com").unwrap();
let mut headers = HashMap::new();
headers.insert("User-Agent","Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36");
let res = http.headers(headers).send().unwrap();
println!("status code {}",res.status_code());
```

### support https
```rust
use minihttp::request::Request;

let mut http = Request::new("https://www.google.com").unwrap();
let res = http.get().send().unwrap();
```

### support proxy
```rust
use minihttp::request::Request;

let mut http = Request::new("http://www.google.com").unwrap();
let res = http.proxy("http://127.0.0.1:1080").unwrap().get().send().unwrap();
println!("status code {}",res.status_code());
```
