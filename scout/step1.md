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


