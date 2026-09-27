# Coding Assignment 1 - Docker File

## Student Information

**Student Name:** Khushdeep Kaur

## Project Overview

This project is a React web application created using Create React App and deployed inside a Docker container.

The purpose of this assignment is to demonstrate how to create a React application, configure a Dockerfile, build a Docker image, create and run a Docker container, configure a WORKDIR, map ports, and access the application through localhost.

The web application displays the following heading:

```html
<h1>Codin 1</h1>
```

The final Dockerized application can be accessed at:

```text
http://localhost:7775
```

---

## Prerequisites

Before creating the project, I made sure the following software was installed on my computer:

- Node.js
- npm
- npx
- Docker Desktop
- Git
- Visual Studio Code

I verified the installations using the following commands:

```bash
node --version
npm --version
npx --version
docker --version
git --version
```

---

## Step 1 - Create the React Application

I created a project folder and opened it in Visual Studio Code.

I used Create React App to create the React development environment with the following command:

```bash
npx create-react-app .
```

`npx` allows a Node package to be executed without installing it globally. In this project, it was used to execute Create React App.

`npm` is the Node Package Manager. It is used to install and manage the packages and dependencies required by the React application.

---

## Step 2 - Configure the React Application

After creating the React application, I opened the `src/App.js` file.

I modified the App component so that the web application displays the required H1 heading:

```jsx
function App() {
  return (
    <div>
      <h1>Codin 1</h1>
    </div>
  );
}

export default App;
```

I tested the React application locally using:

```bash
npm start
```

This confirmed that the React application was working correctly before creating the Docker container.

---

## Step 3 - Create the Dockerfile

I created a file named `Dockerfile` in the root directory of the project.

The Dockerfile contains:

```dockerfile
FROM node:18-alpine

WORKDIR /kaur_khushdeep_site

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "start"]
```

---

## Step 4 - Dockerfile Explanation

### FROM

```dockerfile
FROM node:18-alpine
```

This specifies the base Docker image. It provides the Node.js environment required to install the dependencies and run the React application.

### WORKDIR

```dockerfile
WORKDIR /kaur_khushdeep_site
```

`WORKDIR` sets the working directory inside the Docker container.

For this assignment, my working directory is:

```text
/kaur_khushdeep_site
```

All subsequent Dockerfile commands are executed relative to this directory.

### COPY package files

```dockerfile
COPY package*.json ./
```

This copies the package files from the project into the working directory inside the Docker image.

### RUN npm install

```dockerfile
RUN npm install
```

This installs the npm dependencies required by the React application inside the Docker image.

### COPY project files

```dockerfile
COPY . .
```

This copies the remaining project files into the Docker image.

### EXPOSE

```dockerfile
EXPOSE 3000
```

The React development server runs on port 3000 inside the Docker container.

### CMD

```dockerfile
CMD ["npm", "start"]
```

This command starts the React development server when the Docker container starts.

---

## Step 5 - Build the Docker Image

I built the Docker image using:

```bash
docker build -t coding-assignment11 .
```

The `docker build` command creates a Docker image using the instructions in the Dockerfile.

The `-t` option assigns a name/tag to the image.

The final `.` tells Docker to use the current directory as the build context.

A Docker image is a packaged template containing the application, dependencies, and configuration required to create a Docker container.

---

## Step 6 - Create and Run the Docker Container

I created and ran the Docker container using:

```bash
docker run --name kaur_khushdeep_coding_assignment11 -p 7775:3000 coding-assignment11
```

The container name is:

```text
kaur_khushdeep_coding_assignment11
```

A Docker container is a running instance of a Docker image.

---

## Step 7 - Port Mapping

The following option is used in the `docker run` command:

```text
-p 7775:3000
```

This maps port `7775` on the host computer to port `3000` inside the Docker container.

The React application runs on port 3000 inside the container, but it can be accessed from the host computer using port 7775.

The port mapping is:

```text
Host Port 7775 -> Container Port 3000
```

---

## Step 8 - Access the Application

After starting the Docker container, I opened the following address in a web browser:

```text
http://localhost:7775
```

The application successfully displays:

```text
Codin 1
```

This confirms that the React application is running successfully inside the Docker container and that the port mapping is working.

---

## Step 9 - Verify the Running Container

I used the following command to verify that the container was running:

```bash
docker ps
```

The container appears with the required name:

```text
kaur_khushdeep_coding_assignment11
```

The port mapping shows that host port 7775 is mapped to container port 3000.

---

## Step 10 - Verify the WORKDIR

I entered the running container using:

```bash
docker exec -it kaur_khushdeep_coding_assignment11 sh
```

Inside the container, I used:

```bash
pwd
```

The output was:

```text
/kaur_khushdeep_site
```

This confirms that the Docker WORKDIR was configured correctly.

I exited the container shell using:

```bash
exit
```

---

## Important Docker Concepts

### Dockerfile

A Dockerfile is a text file containing instructions that Docker uses to build a Docker image.

### Docker Image

A Docker image is a packaged template containing the application, dependencies, and configuration required to create a container.

### Docker Container

A Docker container is a running instance of a Docker image.

### WORKDIR

WORKDIR specifies the working directory inside the Docker container.

### Port Mapping

Port mapping connects a port on the host computer to a port inside the Docker container.

For this project:

```text
localhost:7775 -> container port 3000
```

---

## Final Result

The project meets the assignment requirements:

- React application was created using Create React App.
- The application displays `<h1>Codin 1</h1>`.
- A Dockerfile was created and configured.
- The WORKDIR is `/kaur_khushdeep_site`.
- A Docker image was successfully built.
- A Docker container was successfully created and run.
- The container is named `kaur_khushdeep_coding_assignment11`.
- Host port 7775 is mapped to container port 3000.
- The application runs successfully at `http://localhost:7775`.