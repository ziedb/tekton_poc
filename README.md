# 📦 
# Using tekton pipeline on OpenShift

## 🚀 
## Calling an API

### 1. create tasks and pipeline to curl an URL

```bash
$ oc apply -f tasks/curl-task.yaml

$ oc apply -f pipelines/curl-pipeline.yaml
```

### 2. Run the pipeline and set THE_URL parameter with API url :

```bash
$ tkn pipeline start --use-param-defaults  curl-pipeline -p THE_URL=https://api.my-ip.io/v2/ip.json
```

### 3. Find the name of the pipeline run

```bash
$ tkn pr list
NAME                              STARTED          DURATION   STATUS

curl-pipeline-run-m2llc           12 seconds ago   6s         Succeeded
```
### 4. View the logs of the pipeline :

```bash
$ tkn pr logs curl-pipeline-run-m2llc

[run-curl-task : curl-url]   % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current

[run-curl-task : curl-url]                                  Dload  Upload   Total   Spent    Left  Speed

100   256  100   256    0     0   1592      0 --:--:-- --:--:-- --:--:--  1590

[run-curl-task : curl-url] {"success":true,"ip":"X.X.X.X","type":"IPv4","country":{"code":"FR","name":"France"},"region":"Paris","city":"Paris","location":{"lat":48.8558,"lon":2.3494},"timeZone":"Europe/Paris","asn":{"number":16276,"name":"OVH SAS","network":"X.X.X.X/16"}}
```

## 🚀 
## Scall down replicats
```bash
$ oc apply -f hello-word.yaml
deployment.apps/hello-world created
                                                                                                                                 ✓

$ oc get pods
NAME                                                READY   STATUS      RESTARTS   AGE
hello-world-58b45c7bb8-d4n5z                        1/1     Running     0          5s
hello-world-58b45c7bb8-hsv47                        1/1     Running     0          5s
hello-world-58b45c7bb8-rdr8v                        1/1     Running     0          5s
scale-down-pipeline-run-dmzlv-scale-down-task-pod   0/1     Completed   0          19m
                                                                                                                                 ✓

$ tkn pipeline start --use-param-defaults scale-down-pipeline -p APP_NAME=hello-world
PipelineRun started: scale-down-pipeline-run-bvfw8

In order to track the PipelineRun progress run:
tkn pipelinerun logs scale-down-pipeline-run-bvfw8 -f -n tektonlab
                                                                                                                                 ✓

$ tkn pipelinerun logs scale-down-pipeline-run-bvfw8 -f -n tektonlab
[scale-down-task : oc] deployment.apps/hello-world scaled

                                                                                                                                 ✓

$ oc get pods
NAME                                                READY   STATUS      RESTARTS   AGE
scale-down-pipeline-run-bvfw8-scale-down-task-pod   0/1     Completed   0          18s
scale-down-pipeline-run-dmzlv-scale-down-task-pod   0/1     Completed   0          24m
```
## 💭 Feedback and Contributing

