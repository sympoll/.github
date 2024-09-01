# Welcome to Sympoll™   
<br />   
   
<img src="https://github.com/user-attachments/assets/21ac4b41-d12e-43b7-80dd-0c7ae80326de" alt="drawing" width="330" align="left" />   
<br />    

### About
**Workshop:** Cloud Native Development with Kubernetes

**Mentor:** Benny Rochwerger

**Project name:** Sympoll

**Group name:** MTAPizza

**Members:** Roy Toledano, Idan Shalom, Ronen Gelmanovich

**Project Track:** Entrepreneurial
   
<br />   

<br />   

<br />   


## What is Sympoll?
Sympoll is an online surveying platform designed for optimal scalability using Kubernetes. It was developed to address the challenges of conducting effective surveys in environments where group conversations can disrupt the survey process.

Sympoll is targeted at a diverse audience, including community organizers, social planners, students, and corporate leaders, providing a streamlined and accessible platform for all types of survey needs.​

<br />    

## Technologies Used:   
<table align="center">
  <tr>
    <td align="center">
      <h3>Frontend Related:</h3>
      <a href="https://github.com/sympoll">
        <img src="https://skillicons.dev/icons?i=react,vite,typescript,css,html&perline=16&theme=light" alt="Frontend Related Skills" />
      </a>
       <br /> 
    </td>
    <td align="center">
      <h3>Backend Related:</h3>
      <a href="https://github.com/Idan-sh">
        <img src="https://skillicons.dev/icons?i=java,spring,maven,postgresql&perline=16&theme=light" alt="Backend Related Skills" />
      </a>
    </td>
    <td align="center">
      <h3>Devops Related:</h3>
      <a href="https://github.com/Idan-sh">
        <img src="https://skillicons.dev/icons?i=kubernetes,git,github,githubactions&perline=16&theme=light" alt="DevOps Related Skills" />
      </a>
    </td>
  </tr>
</table>
<br />   

## Project's Architecture
#### Entry Point:
*   [Frontend Service:](https://github.com/sympoll/front-end-service)

    *	`Role:` Acts as the user interface or API gateway. It handles incoming requests from users or other systems, routes them to the appropriate web page, and communicates with the appropriate backend services to pull/push data from the database.
    * `Service Port:` 8080
   
#### Microservices:
*	[API Gateway:](https://github.com/sympoll/api-gateway-service)   
    *	`Role:` Handles external requests to expose the cluster to the outside world.
    *	`Interaction:` Receives requests from the frontend service, routes them to the service requested according to the endpoint of the request.
      Each request should have the endpoint '/api' with the suffix of the wanted service to communicate with.
    *	`Service Port:` 8081   
         
*	[Poll Service:](https://github.com/sympoll/poll-service)
    *	`Role:` Handles the creation, updating, and management of polls.
    *	`Interaction:` Interfaces with the poll database to store poll data and processes requests from the frontend service.
    *	`Service Port:` 8082
    *	`DB Port:` 5432:5432 (external:internal)   
         
*	[User Service:](https://github.com/sympoll/user-service)
    *	`Role:` Manages user-related functionalities, such as user registration, authentication, and profile management.
    *	`Interaction:` Receives requests from the frontend service and interacts with the users database to store and retrieve user data.
    *	`Service Port:` 8083
    *	`DB Port:` 5433:5432 (external:internal)     
         
*	[Vote Service:](https://github.com/sympoll/vote-service)
    *	`Role:` Manages the voting process within the application, including casting votes and tallying results.
    *	`Interaction:` Interacts with the poll management service and the votes database to record and retrieve vote data.
    *	`Service Port:` 8084
    *	`DB Port:` 5434:5432 (external:internal)   
    
*	[Group Service:](https://github.com/sympoll/group-service)
    *	`Role:` Manages groups within the application, such as creating, updating, and deleting groups.
    *	`Interaction:` Communicates with the group database to manage group-related data and receives requests routed through the frontend service.
    *	`Service Port:` 8085
    *	`DB Port:` 5435:5432 (external:internal)
 
*	[Media Service:](https://github.com/sympoll/media-service)
    *	`Role:` Manages media storage within the application. Used mostly for user profile pictures and banners.
    *	`Interaction:` Communicates with the media database to manage image file data and receives requests routed through the frontend service.
      Interacts with the user service to save the user's profile image URLs.
    *	`Service Port:` 8086
    *	`DB Port:` 5436:5432 (external:internal)   



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
This pod can send requests to other pods in the cluster, use commands inside the network, etc.
1. To pull and run the console pod:
```bash
kubectl run --image quay.io/brochwer/console console
```
2. To connect to the console pod to start debugging:
```bash
kubectl exec -ti console -- /usr/bin/bash
```
<br />   
   
Then to check that the DNS is configured correctly:
```bash
nslookup {domain-name}
```
To check logs of a pod (outside of the console pod):
```bash
kubectl logs {pod-full-name}
```
