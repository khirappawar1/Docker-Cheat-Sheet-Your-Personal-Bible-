## Docker Cheat Sheet” (Personal Bible) ##

## Dockerfile structure: 


- FROM -  Select the base image and its version based on the application code, Package.josn files.

- WORKDIR - Create the working directory for conatiner (everything happnes inside the directory)

- COPY - Copy the dependencies inside the working directory(package*.json/requirements.txt,etc)

- RUN - Run command used while creating the container (use to build/insatll dependencies that copied 

inside the working directory)

- EXPOSE - See the application code and expose the container port for the application

- CMD / ENTRYPOINT - These command used to run when conatiner/image is created (check the package.json file>under scripts file or code mentioned run in this command)



## You see:
server.js
routes/user.js
mongoose.connect(...)

👉 Decision:

Backend → Node base image
No multi-stage needed
Create backend/Dockerfile

## You also see:
src/App.jsx
npm run build

👉 Decision:
Frontend → Multi-stage Dockerfile
Node (build) → Nginx (serve)


## You see:
MongoDB URI in .env

👉 Decision:
Use mongo:latest in docker-compose.yml

## Docker Compose structure:

- services - Defines all containers in the application.Each service = one container (backend, frontend, db)

- build - Specifies how to build an image from a Dockerfile.

build: ./backend

- ports - Maps container ports to host machine ports.

ports:
  - "5000:5000"

- environment - Sets environment variables inside the container.

environment:
  - NODE_ENV=production

- depends_on - Defines service startup order.

depends_on:
  - mongo

- healtchecks - you can add health check for Database app.

- volumes - Persists or shares data between host and container.

volumes:
  - mongo-data:/data/db

- network - Bridge/host network

networks:
  app-network:

## Rebuild MERN Setup from Scratch (Weekly)

Once a week:

Don’t reuse old code
Recreate:
Backend Dockerfile
Frontend Dockerfile
Mongo container
docker-compose.yml

👉 This forces memory reinforcemen

## Use Pattern-Based Learning (Instead of Memorizing)


* Example pattern for backend Dockerfile:

- Base image → setup → install deps → copy code → run app

Example pattern for compose:

- Each service = container
Services communicate via service name (DNS)
