json_server_test
================
Simple test of deploying a json_server_test with a db.json file
* locally using docker
* remotely using kubernetes

Deploying locally 
-----------------

```bash
> docker build -t $(whoami)/json_server_test:v1 .
> docker run -d -p 80:80 $(whoami)/json_server_test:v1
> curl http://localhost | jq
```

Deploying to Kubernetes
-----------------------

```bash
> kubectl create configmap json-server-test-config --from-file=db.json
> kubectl create -f deployment.yaml
> kubectl expose deployment json-server-test --type=ClusterIP --port=80 --target-port=80
> kubectl create -f ingress.yaml
> curl http://status.discoos.io/db | jq
```
