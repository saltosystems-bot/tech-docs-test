---
title: "Errors"
---

SALTO Nebula uses gRPC error codes to indicate the success or failure of an API request.

## Summary of status codes

|gRPC Code|Meaning|Description|
|---|---|---|
|0|OK|Success|
|3|Invalid Argument|The request was unacceptable, often due to missing a required parameter|
|5|Not Found|The requested resource does not exist|
|13|Internal|Internal errors. This means that some invariants expected by the underlying system have been broken. This error code is reserved for serious errors|
|16|Unauthenticated|The request has not been applied because it lacks valid credentials for the target resource|
