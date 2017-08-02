# raven

raven is a Go client for the [Sentry](https://github.com/getsentry/sentry)
event/error logging system.

- [**API Documentation**](https://godoc.org/github.com/getsentry/raven-go)
- [**Usage and Examples**](https://docs.sentry.io/clients/go/)

## Fork information
This repo is forked from [Sentry Client in Go](https://github.com/getsentry/raven-go) 
commit : [d175f85701dfbf44cb0510114c9943e665e60907](https://github.com/getsentry/raven-go/commit/d175f85701dfbf44cb0510114c9943e665e60907)

## Objective
Official Sentry Client in Go doesn't support LEVEL definition such as DEBUG, INFO, WARNING, ERROR or FATAL. 
Adding new function to pass LEVEL when initialize Sentry packet. 

## Installation

```text
go get github.com/stevenon1003/raven-go
```

If you use dep, type following after `go get`

```
dep ensure github.com/stevenon1003/raven-go@sentry-level
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