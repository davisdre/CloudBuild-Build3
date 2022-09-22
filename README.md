# Introduction 
In this cloud build we will be utilizing GCP. We will be getting familiarize with Cloud Run GUI, and cli via Cloud Shell.
We will be deploying two Cloud Run services. First, a Hello World container to help us learn the Cloud Run GUI. Second, import a public image from Docker Hub to help us learn the gCloud CLI.

# Getting Started
The following will help you get started with this build:

1. Have either a [GCP free account](https://cloud.google.com/free/) or an account like [A Cloud Guru account](https://acloudguru.com/) that has a cloud playground/sandbox environment.

# Build and Test
## Step 1
Lets sign into the GCP portal, https://cloud.google.com.

## Step 2
Lets create a project.
1. click 'New project'
2. create a project name
3. Click 'Create' 

![Screenshot for step 2](/step2.PNG)

## Step 3
Lets Deploy to Cloud run via GUI.
1. lets me sure we selected our new project 
2. click 'cloud run' on left nav bar
3. enable cloud run if not already enabled.
4. click 'create service'.
5. select 'deploy one revision from an existing container image.'
6. click 'test with a sample container' which is a Docker Hello World container.
7. can leave service name default or customize it to your liking
8. set region to 'us-east1'
9. for autoscaling set 'maximum number of instances' to '1'.
10. select 'Allow unauthenticat invocations'.
11. click Create. (NOTE, this process can take up to 5 minutes).
12. now click on the URL and see if your container is running now. 
13. now lets go back and clean up our resources. 

![Screenshot 1 for step 3](/step3.PNG)

![Screenshot 2 for step 3](/step3.12.PNG)

## Step 4
Lets Deploy to Cloud Run via gcloud using a Public image and have some fun.
1. lets activate our Cloud Shell. 
2. Lets open our Cloud Shell in a new window just for better viewing experience.
3. verify that the cloud shell is running in the project you created. 
4. lets setup some default settings for Cloud Run:
     ``` BASH 
    gcloud config set run/platform managed # set Cloud Run to use a managed platform

    gcloud config set run/region us-east1 # set Cloud Run use us-east1 region

    gcloud auth configure-docker # set docker authentication

    docker pull mattipaksula/http-doom # grab the public image

    docker tag mattipaksula/http-doom gcr.io/your-project-name/http-doom # tag it with a new name for gcr.io

    docker push gcr.io/your-project-name/http-doom # we are now sending our image to google container registry

    # deploy our Cloud Run Service
    gcloud run deploy http-doom \
    --image gcr.io/your-project-name/http-doom \
    --cpu=2 \
    --max-instances=1 \
    --memory=4Gi \
    --allow-unauthenticated
    ```
5. now click on the URL and we can have some fun!
6. now lets go back to GUI and clean up resources.

![Screenshot for step 4](/step4.PNG)

## Step 5
Now lets go back to GUI and clean up our project
1. go to 'manage resources' 
2. check box the project name and click delete.

![Screenshot for step 5](/step5.PNG)

# Resource Link
- https://cloud.google.com/run/docs/quickstarts/deploy-container
- https://cloud.google.com/run/docs/overview/what-is-cloud-run
- https://help.acloud.guru/hc/en-us/articles/360001389276?_ga=2.110666693.1947094082.1663603873-1476531138.1660764520
- https://cloud.google.com/sdk/gcloud/reference/config/set