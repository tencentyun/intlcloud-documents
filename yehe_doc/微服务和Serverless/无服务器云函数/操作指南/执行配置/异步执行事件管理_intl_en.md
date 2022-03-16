SCF provides the features of getting the list and status of and terminating asynchronously executed function events for easier event management.

>! Features involved in this document are supported only for [asynchronously executed](https://intl.cloud.tencent.com/document/product/583/39466) functions.

## Getting Async Event List and Status

An asynchronously executed function event has the following status:

- Running: the event is being executed asynchronously.
- Invoked successfully: the event is asynchronously executed successfully with a normal response.
- Invocation failed: the event failed to be asynchronously executed with an exceptional response.
- Invocation terminated: the user actively terminated the event in progress, and async execution stopped.

### Relevant APIs

<table>
<thead>
<tr>
<th>API</th>
<th>Description</th>
<th>Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>ListAsyncEvents</td>
<td>This API lists the information of an asynchronously executed event. It can query the information by conditions such as `RequestId`, function name, function version, event status, and event invocation/end time.
<dx-alert infotype="notice" title="">
Only data within three days after event tracking is enabled can be queried.
</dx-alert>
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/583/39734">ListAsyncEvents</a></td>
</tr>
<tr>
<td>GetAsyncEventStatus</td>
<td>This API is used to get the async event execution status based on the `RequestId`. The event status will be retained for 72 hours (after the end of the event).</td>
<td>GetAsyncEventStatus</a></td>
</tr>
</tbody>
</table>

>! When using an API, pay attention to the API call rate limit. We recommend you not call the `ListAsyncEvents` API frequently. To query the execution result of an async event, call the `GetAsyncEventStatus` API instead.

## Terminating async function event

SCF provides two async event termination methods: **terminating invocation** and **sending termination signal**, whose differences and usage are as detailed below:

### Relevant APIs

<table>
<thead>
<tr>
<th>API</th>
<th>Description</th>
<th>Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>TerminateAsyncEvent</td>
<td>This API is used to terminate an asynchronously executed event in progress according to the returned `RequestId`. The default behavior of this API is to terminate invocation. If the `GraceShutdown` parameter is set to `True`, the `SIGTERM` termination signal will be sent to the request. You can listen on the signal and customize the signal processing logic inside the function.</td>
<td><a href="https://intl.cloud.tencent.com/zh/document/product/583/39733">TerminateAsyncEvent</a></td>
</tr>
</tbody>
</table>



### Terminating invocation

When a function is invoked, SCF will assign an instance to process the function request or event. After the function code is executed and its response is returned, the instance will process other requests. If all instances are running when a request arrives, SCF will assign a new concurrent instance. For more information on instances, see [Concurrency Overview](https://intl.cloud.tencent.com/document/product/583/37040).

After the asynchronously executed function event receives the invocation termination instruction, SCF will forcibly stop instance operations and repossess the instance. When the next request arrives, if there are no idle instances, SCF will assign a new instance to process the request.

**Use cases**

This method is suitable for scenarios where function execution needs to be stopped in advance, such as infinite loop and execution exception of an asynchronously executed function.

**Notes**

Invocation termination will forcibly terminate an instance and trigger instance repossession, which means that cached information in the instance cannot be obtained normally (such as files in the `/tmp` folder). If you want to use this feature, promptly write the files in the instance cache to other persistent storage media to avoid file loss after instance repossession.

### Sending termination signal

When you call the `TerminateAsyncEvent` API and set the `GraceShutdown` parameter to `True`, SCF will send the termination signal `SIGTERM` to the event specified in the input API parameter. You can listen on the signal and customize the processing logic after receiving the signal, including but not limited to function execution termination.

After an asynchronously executed function event receives the `SIGTERM` signal:

- If a signal processing function is defined and listened on in the function code, the corresponding signal processing function logic will be executed.
- If the signal isn't listened on in the function code, the function process will exit and return the error code 439 (`User process exit when running`, indicating that the user process exits).
- SCF records the event signal reception conditions into the function execution log:
  - Received the signal successfully: "[PLATFORM] Signal received successfully" will be logged.
  - Failed to receive the signal: "[PLATFORM] Signal reception failed" will be logged.

#### Use cases

This method is suitable for scenarios where function execution needs to be stopped for business requirements and custom processing logic needs to be run before the stop.

#### Usage

The following sample code describes how to use a custom signal processing function to stop function execution after the `SIGTERM` signal is listened on:


#### Code deployment


<dx-codeblock>
::: Python python
# -*- coding: utf8 -*-
import time
import signal

class GracefulKiller:
	kill_now = False
	def __init__(self):
    # Register signal processing function
		signal.signal(signal.SIGTERM, self.graceshutdown)
	def graceshutdown(self, *agrg):
		print("do something before shutdown.")
		self.kill_now = True

def main_handler(event, context):
	killer = GracefulKiller()

	while not killer.kill_now:
		time.sleep(1)
		print(killer.kill_now)
	    
	print("Graceful shutdown.")
	return("END")
:::
::: Golang golang
package main

import (
	"context"
	"fmt"
	"log"
	"os"
	"os/signal"
	"syscall"
	"time"

	"github.com/tencentyun/scf-go-lib/cloudfunction"
)

type DefineEvent struct {
	// test event define
	Key1 string `json:"key1"`
	Key2 string `json:"key2"`
}

func hello(ctx context.Context, event DefineEvent) (string, error) {
	go graceshutdown()
	sleepNum := 0
	for {
		sleepNum++
		fmt.Println("sleep:", sleepNum)
		time.Sleep(time.Second)
	}
}

// Register signal processing function
func graceshutdown() {
	sigs := make(chan os.Signal, 1)
	signal.Notify(sigs, syscall.SIGTERM)
	sig := <-sigs
	log.Printf("receive signal %s", sig.String())
	//do something before shutdown.
	os.Exit(0)
}

func main() {
	// Make the handler available for Remote Procedure Call by Cloud Function
	cloudfunction.Start(hello)
}
:::
</dx-codeblock>




#### Image deployment
Python
<dx-codeblock>
::: Python python
# -*- coding: utf8 -*-
from flask import Flask, request
import time
import signal
app = Flask(__name__)

class GracefulKiller:
	kill_now = False
	def __init__(self):
    # Register signal processing function
		signal.signal(signal.SIGTERM, self.graceshutdown)
	def graceshutdown(self, *agrg):
		print("do something before shutdown.")
		self.kill_now = True

@app.route('/event-invoke', methods = ['POST'])
def invoke():
	while not killer.kill_now:
		time.sleep(1)
		print(killer.kill_now)

	print("Graceful shutdown.")
	return("END")

if __name__ == '__main__':
    killer = GracefulKiller()
    app.run(host='0.0.0.0', port=9000)
:::
</dx-codeblock>

