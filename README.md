# server-client

Its a demo project to build a basic deployment mechanism for the classic t3 app

# Workflow

Deployment process is executed in the following order:
* Push to master triggers the pipeline
* Pipeline builds backend & frontend images and forwards pushes them to the docker.io repository
* Pipeline provisions the target kubernetes cluster in gke with terraform
* Pipeline authenticates to the provisioned cluster and deploys the whole setup as a tightly coupled helm chart
* Helm chart takes care of configuring apps as a bundle to run them together out of the box

# Run locally

* [Install helm](https://helm.sh/docs/intro/install/)
* Ensure the access to kubernetes cluster 
* Deploy chart 
```bash
helm install server-client ./helm --dependency-update -i
```

# Notes 
This setup uses a pretty dirty helm chart and exposed secret values which makes it dangerous and unusable for the prod environment.  Also, such a tight coupling should not take place when running an enterprise system due to scalability complications and flaws. 