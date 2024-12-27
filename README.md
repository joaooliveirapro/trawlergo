# Trawlergo 🐛
Basic HTTP crawler in Golang. Use this to find out all the URLs for given domain along with related information from the HTTP request.

## Features
- Regex match to include/exclude paths
- Concurrency safe
- HTTP Request information includes:
    - Response status code
    - Added count (how many new links fonund on page)

## Install
```sh
$ go get github.com/joaooliveirapro/trawlergo # install
$ go mod tidy                                 # clean up dependencies
```

## How to use
```go
tg := trawlergo.App{
	Workers:2,                                        // Number of Go routines 
	MaxDepth: 1000,                                   // Max HTTP requests (safe stop)
	Domain: "www.mysite.com",                         // To standardize relative URLs. Don't include the protocol
	StartingURLs, []string{"https://www.mysite.com/"} // Starting URLs
	ExcludeRegex  []string{"/no-go", "[\d]"}          // Don't include these paths
	IncludeRegex  []string{"/some-path-001"}          // Include these paths
}
tg.Run()
tg.SaveToJSON("data.json")
```
<div style="background-color: #fff3cd; border: 1px solid #ffecb5; padding: 10px;">
App must have as many StartingURLs as Workers set to avoid premature exit of Workers. 
</div>

###
```json
// data.json
[
 {
  "addedCount": 3,
  "statusCode": 200,
  "url": "https://crawler-test.com/mobile/separate_desktop_with_different_h1"
 },
 {
  "addedCount": 0,
  "statusCode": 200,
  "url": "https://crawler-test.com/mobile/separate_desktop_with_different_links_in"
 },
 ...
]

```

### License
The MIT License (MIT)