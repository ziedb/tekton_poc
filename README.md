#sh 📦 
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
$ tkn pr logs curl-pipeline-run-m2llci

[run-curl-task : curl-url]   % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current

[run-curl-task : curl-url]                                  Dload  Upload   Total   Spent    Left  Speed

100   256  100   256    0     0   1592      0 --:--:-- --:--:-- --:--:--  1590

[run-curl-task : curl-url] {"success":true,"ip":"92.222.228.153","type":"IPv4","country":{"code":"FR","name":"France"},"region":"Paris","city":"Paris","location":{"lat":48.8558,"lon":2.3494},"timeZone":"Europe/Paris","asn":{"number":16276,"name":"OVH SAS","network":"92.222.0.0/16"}}
```

## 💭 Feedback and Contributing

