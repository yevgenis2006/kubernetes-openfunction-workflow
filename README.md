<img width="1387" height="781" alt="image" src="https://github.com/user-attachments/assets/984954cc-ce3c-4aa5-acc2-6cbc085041da" />


###  OpenFunction | Kubernetes ☸️
OpenFunction is a cloud-native open source FaaS (Function as a Service) platform aiming to let you focus on your business logic without having to maintain the underlying runtime environment and infrastructure. You only need to submit business-related source code in the form of functions.


🧱 Key Features:
```
✅ Cloud agnostic and decoupled with cloud providers' BaaS
✅ Pluggable architecture that allows multiple function runtimes
✅ Support both sync and async functions
✅ Unique async functions support that can consume events directly from event sources
✅ Support generating OCI-Compliant container images directly from function source code.
✅ Flexible autoscaling between 0 and N
✅ Advanced async function autoscaling based on event sources' specific metrics
✅ Simplified BaaS integration for both sync and async functions by introducing Dapr
✅ Advanced function ingress & traffic management powered by K8s Gateway API
✅ Flexible and easy-to-use events management framework
```


### Example 
```
apiVersion: core.openfunction.io/v1beta1
kind: Function
metadata:
  name: function-sample
spec:
  version: "v2.0.0"
  image: "openfunctiondev/sample-go-func:v1"
  imageCredentials:
    name: push-secret
  build:
    builder: openfunction/builder-go:latest
    env:
      FUNC_NAME: "HelloWorld"
      FUNC_CLEAR_SOURCE: "true"
    srcRepo:
      url: "https://github.com/OpenFunction/samples.git"
      sourceSubPath: "functions/knative/hello-world-go"
      revision: "main"
      credentials:
         name: git-repo-secret
  serving:
    template:
      containers:
        - name: function # DO NOT change this
          imagePullPolicy: IfNotPresent 
    runtime: "knative"
```


🔨 Config :
```
terraform init
terraform validate
terraform plan -var-file="template.tfvars"
terraform apply -var-file="template.tfvars" -auto-approve
```
