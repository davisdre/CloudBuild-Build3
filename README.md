# Introduction 
In this cloud build we will be utilizing GCP. We will be getting familiarize with Cloud Run, the GCP console itself, and commandline via Cloud Shell.
We will be deploying two Cloud Run services. One, a Hello World container to help us learn the GUI. Two, import a public image from Docker Hub to help us learn the CLI.

# Getting Started


# Build and Test
1. Lets sign into the portal. https://cloud.google.com

2. Lets create a project.
2.1 project name drew-cloudbuild-sep-2022-pr
2.2 select 'Create'
2.3 select new project. 

3. Lets Deploy to Cloud run via GUI.
3.1 select cloud run on left nav bar
3.2 enable cloud run if not already enabled.
3.3 click create service.
3.4 select 'deploy one revision from an existing container image.'
3.5 click 'test with a sample container' which is a Docker Hello World container.
3.6 can leave service name default or customize it to your liking
3.7 set region to us-east1
3.8 for autoscaling set 'maximum number of instances' to '1'.
3.9 select 'Allow unauthenticat invocations'.
3.10 click Create. (NOTE, this process can take up to 5 minutes).
3.11 now click on the URL and see if your container is running now. 
3.12 now lets go back and clean up our resources. 

4. Lets Deploy to Cloud Run via gcloud using a Public image and have some fun.
4.1 lets activate our Cloud Shell. 
4.2 Lets open our Cloud Shell in a windows just for better experience.
4.3 verify that the cloud shell is running in the project you created. 
4.4 lets setup some default settings for Cloud Run:
4.4.1 gcloud config set run/platform managed # set Cloud Run to use a managed platform
4.4.2 gcloud config set run/region us-east1 # set Cloud Run use us-east1 region
4.4.3 gcloud auth configure-docker # set docker authentication
4.5 docker pull mattipaksula/http-doom # grab the public image
docker tag mattipaksula/http-doom gcr.io/your-project-name/http-doom # tag it with a new name for gcr.io
docker push gcr.io/your-project-name/http-doom # we are now sending our image to google container registry
gcloud run deploy http-doom --image gcr.io/your-project-name/http-doom --cpu=2 --max-instances=1 --memory=4Gi --allow-unauthenticated
4.6 now click on the URL and we can have some fun!
4.7 now lets go back to GUI and clean up resources.
4.8 now lets go back to GUI and clean up our project
4.8.1 go to 'manage services' 
4.8.2 check box the project name and click delete. 

# Resource Link
https://cloud.google.com/run/docs/quickstarts/deploy-container
https://cloud.google.com/run/docs/overview/what-is-cloud-run
https://help.acloud.guru/hc/en-us/articles/360001389276?_ga=2.110666693.1947094082.1663603873-1476531138.1660764520
https://cloud.google.com/sdk/gcloud/reference/config/set