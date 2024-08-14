#TODO


## Python
```python
from hello import exports
from hello.types import Ok
from hello.imports.types import (
    IncomingRequest, ResponseOutparam,
    OutgoingResponse, Fields, OutgoingBody
)

class IncomingHandler(exports.IncomingHandler):
    def handle(self, _: IncomingRequest, response_out: ResponseOutparam):
        # Construct the HTTP response to send back
        outgoingResponse = OutgoingResponse(Fields.from_list([]))
        # Set the status code to OK
        outgoingResponse.set_status_code(200)
        outgoingBody = outgoingResponse.body()
        # Write our Hello World message to the response body
        outgoingBody.write().blocking_write_and_flush(bytes("Hello from Python!\n", "utf-8"))
        OutgoingBody.finish(outgoingBody, None)
        # Set and send the HTTP response
        ResponseOutparam.set(response_out, Ok(outgoingResponse))


```
## Rust
```rust 
wit_bindgen::generate!({
    world: "hello",
});

use exports::wasi::http::incoming_handler::Guest;
use wasi::http::types::*;

struct HttpServer;

impl Guest for HttpServer {
    fn handle(_request: IncomingRequest, response_out: ResponseOutparam) {
        let response = OutgoingResponse::new(Fields::new());
        response.set_status_code(200).unwrap();
        let response_body = response.body().unwrap();
        response_body
            .write()
            .unwrap()
            .blocking_write_and_flush(b"Hello from Rust!\n")
            .unwrap();
        OutgoingBody::finish(response_body, None).expect("failed to finish response body");
        ResponseOutparam::set(response_out, Ok(response));
    }
}

export!(HttpServer);

```
## Golang - OLD

```go 
package main

import (
	http "github.com/wasmcloud/wasmcloud/examples/golang/components/http-hello-world/gen"
)

// Helper type aliases to make code more readable
type HttpRequest = http.ExportsWasiHttp0_2_0_IncomingHandlerIncomingRequest
type HttpResponseWriter = http.ExportsWasiHttp0_2_0_IncomingHandlerResponseOutparam
type HttpOutgoingResponse = http.WasiHttp0_2_0_TypesOutgoingResponse
type HttpError = http.WasiHttp0_2_0_TypesErrorCode

type HttpServer struct{}

func init() {
	httpserver := HttpServer{}
	// Set the incoming handler struct to HttpServer
	http.SetExportsWasiHttp0_2_0_IncomingHandler(httpserver)
}

func (h HttpServer) Handle(request HttpRequest, responseWriter HttpResponseWriter) {
	// Construct HttpResponse to send back
	headers := http.NewFields()
	httpResponse := http.NewOutgoingResponse(headers)
	httpResponse.SetStatusCode(200)
	body := httpResponse.Body().Unwrap()
	bodyWrite := body.Write().Unwrap()
	bodyWrite.BlockingWriteAndFlush([]uint8("Hello from Go!\n")).Unwrap()

	// Send HTTP response
	okResponse := http.Ok[HttpOutgoingResponse, HttpError](httpResponse)
	bodyWrite.Drop()
	http.StaticOutgoingBodyFinish(body, http.None[http.WasiHttp0_2_0_TypesTrailers]())
	http.StaticResponseOutparamSet(responseWriter, okResponse)
}

//go:generate wit-bindgen tiny-go wit --out-dir=gen --gofmt
func main() {}

```
## Golang - New 
[See Full example here](https://wasmcloud.com/blog/compile-go-directly-to-webassembly-components-with-tinygo-and-wasi-p2)

```go
import (
	"encoding/json"
	"math"
	"math/big"
	"strings"
)

func normalizeNumber(v json.Number) any {
	if i, err := v.Int64(); err == nil && math.MinInt <= i && i <= math.MaxInt {
		return int(i)
	}
	if strings.ContainsAny(v.String(), ".eE") {
		if f, err := v.Float64(); err == nil {
			return f
		}
	}
	if bi, ok := new(big.Int).SetString(v.String(), 10); ok {
		return bi
	}
	if strings.HasPrefix(v.String(), "-") {
		return math.Inf(-1)
	}
	return math.Inf(1)
}
```
## Typescript
```ts 
import { IncomingRequest, ResponseOutparam, OutgoingResponse, Fields } from 'wasi:http/types@0.2.0';

// Implementation of wasi-http incoming-handler
//
// NOTE: To understand the types involved, take a look at wit/deps/http/types.wit
function handle(req: IncomingRequest, resp: ResponseOutparam) {
  // Start building an outgoing response
  const outgoingResponse = new OutgoingResponse(new Fields());

  // Access the outgoing response body
  let outgoingBody = outgoingResponse.body();
  {
    // Create a stream for the response body
    let outputStream = outgoingBody.write();
    // Write hello world to the response stream
    outputStream.blockingWriteAndFlush(
      new Uint8Array(new TextEncoder().encode('Hello from Typescript!\n')),
    );
    // @ts-ignore: This is required in order to dispose the stream before we return
    outputStream[Symbol.dispose]();
  }

  // Set the status code for the response
  outgoingResponse.setStatusCode(200);
  // Finish the response body
  OutgoingBody.finish(outgoingBody, undefined);
  // Set the created response
  ResponseOutparam.set(resp, { tag: 'ok', val: outgoingResponse });
}

export const incomingHandler = {
  handle,
};

```