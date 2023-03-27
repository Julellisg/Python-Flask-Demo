# Python Flask Demo
- For COSC 3P95, Question 2. 
- Requires data to be instrumented using OpenTelemetry, implemented in Python.
- Instrumented data should include: traces, metrics, and logs. 
- Data should be visualized, using Jaeger. 
- Source code should have already been included in initial assignment submission on Sakai. 
- Reference: https://opentelemetry.io/docs/instrumentation/python/

## Report
The report for this question can be found [here](https://github.com/Julellisg/Python-Flask-Demo/blob/main/Report.pdf).

## Summary of the Assignment
Below will provide a short overview of what was done for each part of Question 2. 

### Output Files
Both of these files contain the telemetry data that was received during the testing phase. 
They have been split up due to their very large size. 
[Link to traces.txt]()
[Link to metrics.txt]()

### Part A) Choosing a System
After consulting the OpenTelemetry website for support languages, a system was programmed using Python code that uses OpenTelemetry to distrubutes tracing and metric data in a Flask application.

### Part B) Instrumenting the System
The ```opentelemetry-distro``` package installs the API, SDK, and the ```opentelemetry-bootstrap``` and ```opentelemetry-instrument``` tools.

```bash
pip install flask
pip install opentelemetry-distro
```

```bash
opentelemetry-bootstrap -a install
```

Using the following imports, the program is able to utilize OpenTelemetry:
```python
from opentelemetry import trace
from opentelemetry import metrics

from random import randint
from flask import Flask, request
```

Running the instrumented app:
```bash
opentelemetry-instrument \
    --traces_exporter console \
    --metrics_exporter console \
    flask run
```
And you should be prompted with a web address ```http://127.0.0.1:5000``` by default, and by entering the site, you can add ```/rolldice``` to view the specific resource being requested on the server.

### Part C) Visualizing the Telemetry Data
Unfortunately, there was difficulty implemented a backend service to visualize the telemetry data. Telemetry data was found when running the program, however implementing the OpenTelemetry Collector was difficult. 
Part of this effort can be found in the ```/tmp/``` folder contains a ```.yaml``` configuration file. Additionally the following docker code was supposed to be executed. 
```bash
docker run -p 4317:4317 \
    -v /tmp/otel-collector-config.yaml:/etc/otel-collector-config.yaml \
    otel/opentelemetry-collector:latest \
    --config=/etc/otel-collector-config.yaml
```