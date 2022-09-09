Voting App
=========

A distributed application running in Kubernetes, providing two interfaces, one for voting one for seeing the results.

This is based on the original [example-voting-app](https://github.com/dockersamples/example-voting-app) repository.

Architecture
-----

<p align="center">
  <img src="architecture.png">
</p>

* A front-end web app in [Python](/docker/vote) which lets you vote between two options
* A [Redis](https://hub.docker.com/_/redis/) queue which collects new votes
* A [Java](/docker/worker/src/main)  worker which consumes votes and stores them in a Posgres database
* A [Postgres](https://hub.docker.com/_/postgres/) database backed by a Docker volume
* A [Node.js](/docker/result) webapp which shows the results of the voting in real time
* An Ingress in a fanout configuration to route traffic to the corresponding Services based on the HTTP URI being requested.

Run the app in Kubernetes
-------------------------
The folder k8s-specifications contains the yaml specifications of the Voting App's services.


Notes
-----

The voting application only accepts one vote per client. It does not register votes if a vote has already been submitted from a client.


