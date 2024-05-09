# Simpler HTTP Server  

# How it looks like?

### Screenshot
<img src="./screenshot.png" width="80%" height="80%">

### Command Line Arguments
```
Simpler HTTP(s) Server 0.6.9x

USAGE:
    simpler-http-server [FLAGS] [OPTIONS] [--] [root]

FLAGS:
        --coep       Add "Cross-Origin-Embedder-Policy" HTTP header and set it to "require-corp"
        --coop       Add "Cross-Origin-Opener-Policy" HTTP header and set it to "same-origin"
        --cors       Enable CORS via the "Access-Control-Allow-Origin" header
    -h, --help       Prints help information
    -i, --index      Enable automatic render index page [index.html, index.htm]
        --nocache    Disable http cache
        --norange    Disable header::Range support (partial request)
        --nosort     Disable directory entries sort (by: name, modified, size)
    -o, --open       Open the page in the default browser
    -s, --silent     Disable all outputs
    -u, --upload     Enable upload files. (multiple select)
    -V, --version    Prints version information

OPTIONS:
    -a, --auth <auth>                HTTP Basic Auth (username:password)
    -b, --base-url <base-url>        Base URL to prepend in directory indexes. For reverse proxying. This prefix is
                                     supposed to be pre-stripped when reaching simple-http-server. [default: /]
        --cert <cert>                TLS/SSL certificate (pkcs#12 format)
        --certpass <certpass>        TLS/SSL certificate password
    -c, --compress <compress>...     Enable file compression: gzip/deflate
                                         Example: -c=js,d.ts
                                         Note: disabled on partial request!
        --ip <ip>                    IP address to bind [default: 0.0.0.0]
    -p, --port <port>                Port number [default: 8000]
        --redirect <redirect>        takes a URL to redirect to using HTTP 301 Moved Permanently
    -t, --threads <threads>          How many worker threads [default: 3]
        --try-file <PATH>            serve this file (server root relative) in place of missing files (useful for single
                                     page apps) [aliases: try-file-404]
    -l, --upload-size-limit <NUM>    Upload file size limit [bytes] [default: 8000000]

ARGS:
    <root>    Root directory
```

# Installation

### Download binary 
[Goto Download](https://github.com/dw5/simpler-http-server/releases)

 - windows-64bit
 - osx-64bit
 - linux-64bit


### Install by cargo

``` bash
# Install Rust
curl https://sh.rustup.rs -sSf | sh

# Install simpler-http-server
cargo install simpler-http-server
rehash
simpler-http-server -h
```

# Features
- [x] Windows support (with colored log)
- [x] Specify listen address (ip, port)
- [x] Specify running threads
- [x] Specify root directory
- [x] Pretty log
- [x] Nginx like directory view (directory entries, link, filesize, modified date)
- [x] Breadcrumb navigation
- [x] (default enabled) Guess mime type
- [x] (default enabled) HTTP cache control
  - Sending Last-Modified / ETag
  - Replying 304 to If-Modified-Since
- [x] (default enabled) Partial request
  - Accept-Ranges: bytes([ByteRangeSpec; length=1])
  - [Range, If-Range, If-Match] => [Content-Range, 206, 416]
- [x] (default disabled) Automatic render index page [index.html, index.htm]
- [x] (default disabled) Upload file
- [x] (default disabled) HTTP Basic Authentication (by username:password)
- [x] Sort by: filename, filesize, modified date
- [x] HTTPS support
- [x] Content-Encoding: gzip/deflate
- [x] Added CORS headers support
- [x] Silent mode
