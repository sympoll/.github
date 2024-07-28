# Welcome :)
## About
**Workshop:** Cloud Native Development with Kubernetes

**Mentor:** Benny Rochwerger

**Project name:** Sympoll

**Group name:** MTAPizza

**Members:** Roy Toledano, Idan Shalom, Ronen Gelmanovich

**Project Track:** Entrepreneurial


<br />   

## What is Sympoll?
Sympoll is an online surveying platform designed for optimal scalability using Kubernetes. It was developed to address the challenges of conducting effective surveys in environments where group conversations can disrupt the survey process, such as WhatsApp. Sympoll aims to provide a comprehensive solution for various survey needs, integrating a hierarchical polling system with multiple user roles and group functionalities.
Sympoll is targeted at a diverse audience, including community organizers, social planners, students, and corporate leaders, providing a streamlined and accessible platform for all types of survey needs​​.


<br />   

## Project's Architecture
#### Entry Point:
*	**Frontend Service:**
    * Role: Acts as the user interface or API gateway. It handles incoming requests from users or other systems, routes them to the appropriate web page, and communicates with the appropriate backend services to pull/push data from the database.
   
#### Microservices:
*	**User Management Service:**
    *	Role: Manages user-related functionalities, such as user registration, authentication, and profile management.
    *	Interaction: Receives requests from the frontend service and interacts with the database to store and retrieve user data.
*	**Group Management Service:**
    *	Role: Manages groups within the application, such as creating, updating, and deleting groups.
    *	Interaction: Communicates with the database to manage group-related data and receives requests routed through the frontend service.
*	**Poll Management Service:**
    *	Role: Handles the creation, updating, and management of polls.
    *	Interaction: Interfaces with the database to store poll data and processes requests from the frontend service.
*	**Vote Service:**
    *	Role: Manages the voting process within the application, including casting votes and tallying results.
    *	Interaction: Interacts with the poll management service and the database to record and retrieve vote data.


<br />   

## Automated Workflow

- On push to the main branch, a workflow is triggered to automate the building of the container and pushing of its image to our GitHub Packages.
- The versioning of the containers is according to the dates at which they were published to the packages.


<br />   

## Approval Process

- Any push to the main branch requires at least one member of the organization to approve.


<br />   

## Using containers

### Login

In order for you to be able to pull the container image you must first connect your docker to your github account:

```bash
docker login -u {USERNAME} -p {TOKEN} ghcr.io
```

You can generate a token in Github->settings->developer settings->Personal access tokens->Tokens (classic)->Generate new token (classic).

Make sure to:

- name your token with a name indiacting its for your docker.
- Select the write:packages permission.

### Image pull

Once you have successfully connected your docker and github account, pull the image from Github packages.

```bash
docker pull ghcr.io/sympoll/{IMAGE_NAME}:{TAG}
```
   
### Run a container instance

After pulling the image, you can now run a container instance.

```bash
docker run -d --name {CONTAINER_NAME} -p {IMAGE_PORT}:{IMAGE_PORT} -e POSTGRES_PASSWORD={PASSWORD} {IMAGE_HASH}
```

<br />   

## Debugging

### Console pod for debugging the Kubernetes Cluster's Network
For networking debugging inside the Kubernetes Cluster, you can connect to the console pod.   
This pod can send requests to other pods in the cluster, check other pods' logs, etc.
1. To pull and run the console pod:
```bash
kubectl run --image quay.io/brochwer/console console
```
2. To connect to the console pod to start debugging:
```bash
kubectl exec -ti console -- /usr/bin/bash
```
