This document describes how to report the data of a Python application over the Jaeger protocol.

## Directions


### Step 1. Get the endpoint and token

Log in to the [APM console](https://console.cloud.tencent.com/apm), enter the **Application monitoring** > **Application list** page, click **Access application**, and select the Python language and Jaeger data collection method. Then, get the endpoint and token in the step of access method selection.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/5rBD100_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A120230112-120043%402x.png)

### Step 2. Install the Jaeger agent

1. Download the [Jaeger agent](https://github.com/jaegertracing/jaeger/releases/tag/v1.22.0).
2. Run the following command to start the agent:
<dx-codeblock>
:::  sh
nohup ./jaeger-agent --reporter.grpc.host-port={{endpoint}} --jaeger.tags=token={{token}}
:::
</dx-codeblock>

### Step 3. Report data through Jaeger


1. Run the following command to install the `jaeger_client` package.
<dx-codeblock>
:::  sh
pip install jaeger_client
:::
</dx-codeblock>
2. Create the following Python file and tracer object to trace all requests.
<dx-codeblock>
::: Python
from jaeger_client import Config
import time
from os import getenv

# Configure the address of the Jaeger agent, which is the localhost by default.
JAEGER_HOST = getenv('JAEGER_HOST', 'localhost')
SERVICE_NAME = getenv('JAEGER_HOST', 'my_service_test')


def build_your_span(tracer):
    with tracer.start_span('yourTestSpan') as span:
        span.log_kv({'event': 'test your message', 'life': 42})
        span.set_tag("span.kind", "server")
        return span


def build_your_tracer():
    my_config = Config(
        config={
            'sampler': {
                'type': 'const',
                'param': 1,
            },
            'local_agent': {
                'reporting_host': JAEGER_HOST,
                'reporting_port': 6831,
            },
            'logging': True,
        },
        service_name=SERVICE_NAME,
        validate=True
    )
    tracer = my_config.initialize_tracer()

    return tracer


if __name__ == "__main__":
    tracer = build_your_tracer()
    span = build_your_span(tracer)
    time.sleep(2)
    tracer.close()
:::
</dx-codeblock>
<dx-alert infotype="explain" title="">
Currently, Jaeger supports frameworks such as Flask, Django, and gRPC for data reporting. For more information, see the following documents:
- [jaeger-client-python](https://github.com/jaegertracing/jaeger-client-python)
- [3rd-Party OpenTracing API Contributions](https://github.com/opentracing-contrib?q=python&type=&language=&sort=)
</dx-alert>









