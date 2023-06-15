REACT-DOCKER CONFIGURATION IN AWS LINUX EC2 SERVER

Update the package manager repositories by running the following command:
sudo yum update -y

Install nodejs:
sudo yum install nodejs

Install  React Project
npx create-react-app frontend

Install Docker by running the following commands:
sudo yum install -y docker

Start the Docker service:
sudo service docker start

Check information about docker and you can check containers or image is there or not, Running, Paused, Stopped services or not:
sudo docker info


Go inside the project and create Dockerfile
cd frontend
touch Dockerfile
nano Dockerfile

then paste these into the dockerfile
# Use a base image with Node.js installed
FROM node:18.16.0-alpine

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json (if available)
COPY package*.json ./

# Install project dependencies
RUN npm install

# Copy the entire project directory into the container
COPY . .

# Build the React app
RUN npm run build

# Set the startup command to run the React app
CMD ["npm", "start"]

To build the Docker image, make sure you are in the same directory as your Dockerfile and execute the following command:
sudo docker build -t react-app .
To expose a port from your Docker container, you can use the -p or --publish flag when running the container. This flag allows you to map a port on your host machine to a port inside the container.
Here's the syntax to expose a port when running a container:
docker run -p <host-port>:<container-port> your-image-name
sudo docker run -d --name DMS_APP -p 8000:3000 react-app:latest

To see containerId
sudo docker ps -ls
To stop a running Docker container, you can use the docker stop command followed by the container ID or container name. Here's the syntax:
sudo docker stop <container_id_or_name>

If you need to remove the stopped container entirely, you can use the docker rm command. However, please note that this will permanently delete the container and its associated resources. Here's the syntax:
sudo docker rm <container_id_or_name>

To remove a Docker image, you can use the docker rmi command followed by the image ID or image name. Here's the syntax:
sudo docker rmi <image_id_or_name>

To see inside the container
sudo docker exec -it c001f8765516 ls
