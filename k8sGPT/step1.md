> To install K8sGPT, we need to use curl command.
> Click the below command to set it up.
> 

Step 1. Run the following command:

```plain
curl -LO https://github.com/k8sgpt-ai/k8sgpt/releases/download/v0.3.6/k8sgpt_amd64.deb
sudo dpkg -i k8sgpt_amd64.deb
```{{exec}}


Step 2. Verify if K8sGPT is installed correctly

```plain
k8sgpt version
```{{exec}}


Step 3. Generating an API Key from OpenAI

Currently the default AI provider is OpenAI, you will need to generate an API key from OpenAI
You can do this by running k8sgpt generate to open a browser link to generate it

```plain
k8sgpt generate
```{{exec}}

Step 4. Enabling the authentication for OpenAI

Run k8sgpt auth add to set it in k8sgpt.

```plain
k8sgpt auth add
```{{exec}}

Please input the OpenAI Key.

You can also provide the password directly using the --password flag.

Step 5. List the auth

Run k8sgpt auth list the configured providers

```plain
k8sgpt auth list
```{{exec}}

Step 6. Create a YAML file

```plain
echo "apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        resources:
          limits:
            memory: 4Gi" >> deploy.yaml
```{{exec}}

Step 7. Deploy the Pod


```plain
kubectl apply -f deploy.yaml
```{{exec}}


You will notice that Pod consumes more than 4GB that exceeds the default memory size allocated to the instance.



Step 8. Run a Scan

Run k8sgpt analyze to run a scan.

```plain
k8sgpt analyze
```{{exec}}

It should show the error message.

Step 9. Detailed Explanation of the Issues

Use k8sgpt analyze --explain to get a more detailed explanation of the issues

```plain
k8sgpt analyze --explain
```{{exec}}

Step 10. Get the official documentation from Kubernetes.io site

You also run k8sgpt analyze --with-doc (with or without the explain flag) to get the official documention from kubernetes.

```plain
k8sgpt analyze --with-doc
```{{exec}}
