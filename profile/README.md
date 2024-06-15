# Welcome :)
## About
**Workshop:** Cloud Native Development with Kubernetes
**Mentor:** Benny Rochwerger
**Project name:** Sympoll
**Group name:** MTAPizza
**Members:** Roy Toledano, Idan Shalom, Ronen Gelmanovich
**Project Track:** Entrepreneurial

## What is Sympoll?
Sympoll is an online surveying platform designed for optimal scalability using Kubernetes. It was developed to address the challenges of conducting effective surveys in environments where group conversations can disrupt the survey process, such as WhatsApp. Sympoll aims to provide a comprehensive solution for various survey needs, integrating a hierarchical polling system with multiple user roles and group functionalities.
Sympoll is targeted at a diverse audience, including community organizers, social planners, students, and corporate leaders, providing a streamlined and accessible platform for all types of survey needs​​.

## Automated Workflow

- On push to the main branch, a workflow is triggered to automate the building of the container and pushing of its image to our GitHub Packages.
- The versioning of the containers is according to the dates at which they were published to the packages.

## Approval Process

- Any push to the main branch requires at least one member of the organization to approve.

## Using the container

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

<!--

**Here are some ideas to get you started:**

🙋‍♀️ A short introduction - what is your organization all about?
🌈 Contribution guidelines - how can the community get involved?
👩‍💻 Useful resources - where can the community find your docs? Is there anything else the community should know?
🍿 Fun facts - what does your team eat for breakfast?
🧙 Remember, you can do mighty things with the power of [Markdown](https://docs.github.com/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
-->
