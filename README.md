# Kaniko — Building Container Images without the need of Docker daemon

Building containers without Docker may seem like a daunting task, but it is actually a relatively straightforward process that can be accomplished with a few simple tools. In this blog post, we will explore some of the methods and tools available for building containers without Docker daemon.

## Why build containers without Docker?

Although Docker has emerged as the industry norm for containerization, there are situations where you would prefer to create containers without Docker. Here are a few of the main reasons why you might choose an alternative to Docker:

1. Security: Docker requires root access to run, which can introduce security risks.
2. Dependency management: Docker has a large number of dependencies, which can make it difficult to manage in some environments.
3. Flexibility: Docker has a specific way of doing things, which can limit your ability to customize your environment.
4. Compatibility: Some platforms and operating systems may not support Docker, or they may not support the specific version of Docker that you need.
Here we’ll discuss three methods of building container images without Docker daemon

### Buildah 
Buildah is a command-line tool that enables you to create and manipulate containers without the need for Docker. It is a lightweight and flexible tool that can be used in a variety of scenarios.

To use Buildah, you will need to have root access on your system. Once you have installed Buildah, you can use it to create containers from scratch or from existing images. You can then use Buildah to install packages, configure settings, and make other changes to the container.

### Podman 
Podman is another command-line tool that enables you to build and manage containers without Docker. Like Buildah, Podman is designed to be lightweight and easy to use.

To use Podman, you will need to have root access on your system. Once you have installed Podman, you can use it to create containers from scratch or from existing images. You can then use Podman to install packages, configure settings, and make other changes to the container.

### Kaniko
Kaniko is a tool for building container images from a Dockerfile, without requiring a Docker daemon. It is designed to be lightweight and easy to use, and it offers many of the same features as Docker. Kaniko can be used to build containers from scratch, from existing images, or from Dockerfiles.

This blog provides a detailed guide on “How to Create & Manage Container Images Using Kaniko In Windows”.


![maxresdefault](https://miro.medium.com/v2/resize:fit:720/format:webp/0*EIC-A3WqEhyNMfMk.png)


## Prerequisites
To use Kaniko, you will need the following prerequisites:

1. A Dockerfile: Kaniko builds container images from Dockerfiles, so you will need to have a Dockerfile that describes the container image you want to build.
2. Access to a container registry: Once you have built your container image with Kaniko, you will need to push it to a container registry so that it can be used to create new containers or shared with others. You will need to have access to a container registry that supports the Docker registry API.
3. Kaniko executor image: You will need to download the Kaniko executor image from Google Container Registry (GCR).
4. Docker configuration file: Kaniko requires a Docker configuration file that contains the credentials needed to push your container image to a container registry.

## Step 1 : Installing the Kaniko

To install Kaniko, you will need to perform the following steps:

1. Download the Kaniko executor image from Google Container Registry (GCR):

```
docker pull gcr.io/kaniko-project/executor:v1.6.0
```
2. Verify that the Kaniko executor image is downloaded by running the following command:


```
docker images
```
You should see an entry for the gcr.io/kaniko-project/executor image.

3. Create a Dockerfile that describes the container image you want to build. The Dockerfile should be located in a directory that Kaniko can access.

4. Create a Docker configuration file that contains the credentials needed to push your container image to a container registry. The file should be located in a directory that Kaniko can access. For example, you can create a file called config.json with the following contents:

```
{
    "auths": {
        "your.registry.com": {
            "username": "your-username",
            "password": "your-password",
            "email": "your-email"
        }
    }
}
```
Replace your.registry.com, your-username, your-password, and your-email with your actual values.

## Step 2: Build the Container Image
To build a container image with Kaniko, you can use the following command:


```
docker run --rm -v /path/to/build/dir:/workspace -v /path/to/.docker/config.json:/kaniko/.docker/config.json gcr.io/kaniko-project/executor:v1.6.0 --dockerfile=/workspace/Dockerfile --destination=<your-image-name>
```
This command runs the Kaniko executor image and mounts the build directory and Docker configuration file as volumes. The --dockerfile flag specifies the path to your Dockerfile, and the --destination flag specifies the name and tag of the image you want to build.

Once Kaniko has finished building the image, you can push it to a container registry using the docker push command.

## Step 3 : Saving containers as images

Once you have built your container image with Kaniko, you can save it as an image that you can use to create new containers or share with others. You can save the image using the docker save command:

```
docker save <your-image-name> -o <path/to/save/image>
```
This will save the image as a tarball that you can share or use to create new containers.


## Conclusion:
Kaniko is a lightweight and flexible tool that enables you to build container images without the need for a Docker daemon. With Kaniko, you can build containers from scratch, from existing images, or from Dockerfiles, and you can save them as images that you can use in your environment. Whether you’re building specialized containers or just need an alternative to Docker, Kaniko is a great tool to have in your toolbox.

