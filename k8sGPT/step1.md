> To install K8sGPT, we need to use curl command.
> Click the below command to set it up.
> 

Step 1. Run the following command:

```plain
curl -LO https://github.com/k8sgpt-ai/k8sgpt/releases/download/v0.3.13/k8sgpt_amd64.deb
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

Step 4. Enabling the authentication

Run k8sgpt auth add to set it in k8sgpt.

```plain
k8sgpt auth default
```{{exec}}

You can also provide the password directly using the --password flag.

Step 5. List the auth

Run k8sgpt auth list the configured providers

```plain
k8sgpt auth list
```{{exec}}



Step 6. Managing the active filters by the analyzer

Run k8sgpt filters to manage the active filters used by the analyzer. By default, all filters are executed during analysis.

```plain
k8sgpt filters list
```{{exec}}

Step 7. Run a Scan

Run k8sgpt analyze to run a scan.

```plain
k8sgpt analyze
```{{exec}}

Step 8. Detailed Explanation of the Issues

Use k8sgpt analyze --explain to get a more detailed explanation of the issues

```plain
k8sgpt analyze --explain
```{{exec}}

Step 9. Get the official documentation from Kubernetes.io site

You also run k8sgpt analyze --with-doc (with or without the explain flag) to get the official documention from kubernetes.

```plain
k8sgpt analyze --with-doc
```{{exec}}
