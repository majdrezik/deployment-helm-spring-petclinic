# deployment-helm-spring-petclinic

#### This project uses [helm](https://docs.aws.amazon.com/eks/latest/userguide/helm.html) to deploy a project called [PetClinic by Spring](https://github.com/spring-projects/spring-petclinic).
#
#### The Helm package manager for Kubernetes helps you install and manage applications on your Kubernetes cluster. For more information, see the Helm documentation. This topic helps you install and run the Helm binaries so that you can install and manage charts using the Helm CLI on your local system.

#

## How It works

### In [Teamcity](https://www.jetbrains.com/teamcity/), I have a BUILD subproject which builds my Dockerfile (under petclinic-helm-2/Dockerfile) and makes an image out of the build and pushes the image to AWS ECR.

      BUILD STAGE:
        1. BUILD Dockerfile
        2. Tag Image
        3. Push Image to ECR.
 
### In the DEPLOYMENT stage, I use helm to deploy the image from the BUILD stage.

      DEPLOY STAGE:
        1. helm upgrade --install --set imageTag=%dep.PetclinicHelm_Build_2.imageTag% petclinic-helm-2 . -v 20 --debug

Here I recieve the tag from the BUILD stage and pass it to the DEPLOY in order to deploy the latest successful build.
