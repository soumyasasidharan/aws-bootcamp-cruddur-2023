# Week 2 — Distributed Tracing
Distrbuted Tracing with Honeycomb
created trail account on Honeycomb

#Added honeycomb api key

```
$ gp env HONEYCOMB_API_KEY="<API Key>"
HONEYCOMB_API_KEY="<API Key>"
```

#Folliwing code block added to requirements.txt

```
opentelemetry-api 
opentelemetry-sdk 
opentelemetry-exporter-otlp-proto-http 
opentelemetry-instrumentation-flask 
opentelemetry-instrumentation-requests
```
#Added OTEL key to the dockercomposefile.

```
version: "3.8"
services:
    backend-flask:
        environment:
            ...
            ...
            OTEL_SERVICE_NAME: "backend-flask"
            OTEL_EXPORTER_OTLP_ENDPOINT: "https://api.honeycomb.io"
            OTEL_EXPORTER_OTLP_HEADERS: "x-honeycomb-team=${HONEYCOMB_API_KEY}"
```


#try to get traces from honeycomb after adding following code(you will get this codefrom honeycomb)

```
# Honeycomb
from opentelemetry import trace
from opentelemetry.instrumentation.flask import FlaskInstrumentor
from opentelemetry.instrumentation.requests import RequestsInstrumentor
from opentelemetry.exporter.otlp.proto.http.trace_exporter import OTLPSpanExporter
from opentelemetry.sdk.trace import TracerProvider
from opentelemetry.sdk.trace.export import BatchSpanProcessor
```
```
# Initialize tracing and an exporter that can send data to Honeycomb
provider = TracerProvider()
processor = BatchSpanProcessor(OTLPSpanExporter())
provider.add_span_processor(processor)
trace.set_tracer_provider(provider)
tracer = trace.get_tracer(__name__)


app = Flask(__name__)

# Initialize automatic instrumentation with Flask
FlaskInstrumentor().instrument_app(app)
RequestsInstrumentor().instrument()
```
#honeycomb image traces

#Try to get tracing with AWS xray
``
aws-xray-sdk
```
this code block added to the requirements.txt
