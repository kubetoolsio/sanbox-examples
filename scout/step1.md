> To install Docker Scout, we need to use curl command.
> Click the below command to set it up.
> 

## Prerequisite

```plain
  mkdir $HOME/.docker
```{{exec}}


Step 1. Run the following command:

```plain
curl -sSfL https://raw.githubusercontent.com/docker/scout-cli/main/install.sh | sh -s --
```{{exec}}


Step 2. Verify if Docker Scout is installed correctly

```plain
docker scout version
```{{exec}}


Step 3. Clone the repository



```plain
git clone https://github.com/docker/scout-demo-service.git
```{{exec}}

Step 4. Moving into the directory



```plain
cd scout-demo-service
```{{exec}}



Step 5. Export the Docker Hub ORG

Copy the below command and change it with your ORG name


export ORG=<your-Dockerhub-ORG>


Step 6. Create a YAML file

```plain
docker build -t $ORG/scout-demo:v1 .
```{{exec}}

Step 7. Check the vulnerabilities


```plain
docker scout quickview
```{{exec}}


Step 8. Run the below command to filter only vulnerable packages

 ```plain
docker scout cves --only-vuln-packages --format only-packages $ORG/scout-demo:v1
```{{exec}}


Step 9. Fix the vulnerability related to express

```plain
 sed -i 's/"express": "4.17.1"/"express": "4.17.3"/' package.json
```{{exec}}


Step 10. Re-build the Docker Image and tag it with v2


```plain
docker build -t $ORG/scout-demo:v2 .
```{{exec}}


Step 11.  Verify if the vulnerabilities is fixed or not

 ```plain
docker scout cves --only-vuln-packages --format only-packages $ORG/scout-demo:v2
```{{exec}}

Step 12. Push the image to Docker Hub

```plain
docker push $ORG/scout-demo:v2 
```{{exec}}


Step 13. Enable the Scout for this repository

```plain
 docker scout repo enable --org $ORG $ORG/scout-demo
```{{exec}}


Step 13. Access the Scout Dashboard

Open https://scout.docker.com to access the vulnerabilities

<img width="1429" alt="image" src="https://github.com/kubetoolsio/sanbox-examples/assets/142371896/dd2ca592-9eb1-4fd5-bce4-778aab82d0cf">


Step 14. Fixing the base Image Vulnerabilities



```plain
 sed -i '1s/^FROM.*/FROM alpine:3.18/' Dockerfile
```{{exec}}

Step 15. Re-building the Image

```plain
 docker build -t $ORG/scout-demo:v3 .
```

Step 16. Verifying if all the vulnerabilities are fixed

 ```plain
docker scout cves --only-vuln-packages --format only-packages $ORG/scout-demo:v1
```{{exec}}

Step 17. Access the Scout Dashboard

Open https://scout.docker.com to verify if it gets reflected in the dashboard

<img width="1477" alt="image" src="https://github.com/kubetoolsio/sanbox-examples/assets/142371896/581b7885-5cce-4c9f-aee2-4859b67e2d9e">



