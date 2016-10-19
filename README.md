# Gunicorn multi-worker Prometheus example

This example web application shows how you can use Prometheus to monitor Flask web
applications that are deployed using multiple Gunicorn works. To be specific,
it explains how you can emit, collect and expose Prometheus metrics from
multiple Gunicorn worker processes.


## Setup

In a virtualenv, install Flask, Gunicorn and the Python Prometheus client:

    pip install flask gunicorn prometheus-client

## Deployment

Metrics emitted by each worker are stored in a shared directory that has to be
specified upfront using the `prometheus_multiproc_dir` environment variable.

To deploy the example application with 4 Gunicorn worker processes:

    rm -rf multiproc-tmp
    mkdir multiproc-tmp
    export prometheus_multiproc_dir=multiproc-tmp
    gunicorn -c gunicorn_conf.py -w 4 yourapp:app

You are responsible for ensuring the temporary directory exists and is cleaned
up before each deployment.
