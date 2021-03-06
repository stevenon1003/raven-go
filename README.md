# raven

raven is a Go client for the [Sentry](https://github.com/getsentry/sentry)
event/error logging system.

- [**API Documentation**](https://godoc.org/github.com/getsentry/raven-go)
- [**Usage and Examples**](https://docs.sentry.io/clients/go/)

## Fork information
This repo is forked from [Sentry Client in Go](https://github.com/getsentry/raven-go) 
commit : [d5057ceb70caa73feca9ba5d75a8fc00c9dd0aae](https://github.com/getsentry/raven-go/commit/d5057ceb70caa73feca9ba5d75a8fc00c9dd0aae)

## Objective
Official Sentry Client in Go doesn't support LEVEL definition such as DEBUG, INFO, WARNING, ERROR or FATAL. 
Adding new function to pass LEVEL when initialize Sentry packet. 

## Installation

```text
go get github.com/stevenon1003/raven-go
```

If you use dep, type following after `go get`

```
dep ensure -add github.com/stevenon1003/raven-go
```
## How to use

Function name: `raven.CaptureErrorAndWaitWithLevel` `raven.CaptureErrorWithLevel`

Severity: `raven.DEBUG` `raven.INFO` `raven.WARNING` `raven.ERROR` `raven.FATAL`

```
package main

import "github.com/stevenon1003/raven-go"

func init() {
    raven.SetDSN("https://xxxx:yyyy@sentry.io/zzzzzz")
}

//Blocking call 
f, err := os.Open("filename.ext")
if err != nil {
    raven.CaptureErrorAndWaitWithLevel(err, nil, raven.WARNING)
    log.Panic(err)
}

//non-blocking call
raven.CaptureErrorWithLevel(err, nil, raven.INFO)
```