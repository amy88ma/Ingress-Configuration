# Create an Ingress rule for User/Pass Authentication

Protect an Application (eclWatch) with basic authentication, behind NGINX

# Prerequisites
First, install homebrew [here](https://brew.sh).  Then install wget

```
brew install wget
```     

### Create NGINX Controller
```
wget https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.47.0/deploy/static/provider/cloud/deploy.yaml

```
The output should be similar to :
```
20XX-XX-XX 10:27:35 (5.61 MB/s) - ‘deploy.yaml’ saved [18333/18333] 

```
open the file above, and modify type: from LoadBalancer to NodePort
``` 
vi deploy.yaml 

```
Create the controller:
``` 
kubectl apply -f deploy.yaml

```
## Create application
Create application and service

```
kubectl apply -f <name>.yaml

```
## Create a Password file 
contains username and password for users

```
htpasswd -c auth <username>

```
Generate a password when prompted. Run:
```
cat auth

```
to see the password that is generated.

## Use a file to create Ingress rule
This file protects the application.  

```
kubectl create secret generic basic-auth --from-file auth

``` 
Then, apply the rule.
```
kubectl apply -f <name>

```

**Run 'kubectl get secret', which should show the basic authentication created**
## Go to the external IP provided on web browser
```
kubectl get svc -n ingress-nginx

```
### Enter username And Password when prompted