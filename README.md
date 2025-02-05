• Name: Sumeyye Sevgi
• Surname: Kilic
• Student Number: 35436
Project Description
This project is a simple web application that integrates Docker with a frontend, backend, and MongoDB database. The web app allows users to add tasks to a database, which can then be viewed through the backend interface.
Additional Steps to Run the Project
To run the project, follow these steps:


1. Set up Docker Network:
Create a custom Docker network so that all containers (frontend, backend, and MongoDB) can communicate with each other.
```bash
docker network create my-network
```
2. Run the Frontend Container:
The frontend of the web application is served through Nginx. Run the frontend container by binding the local path to the container's Nginx HTML directory.
```bash
docker run --name frontend --network my-network -p 8080:80 -v "C:/path/to/frontend:/usr/share/nginx/html" nginx:alpine
```
Make sure to replace `C:/path/to/frontend` with the actual path to your frontend code.
3. Build and Run the Backend Container:
Build the backend image from the Dockerfile and run it. This container will expose port 3000.
```bash
docker build -t backend-image .
docker run --name backend --network my-network -p 3000:3000 backend-image
```
4. Run the MongoDB Container:
Run the MongoDB container and expose the default MongoDB port (27017). This container is connected to the `my-network` Docker network.
```bash
docker run -d --name mongo --network my-network -p 27017:27017 mongo:latest
```
5. Access MongoDB:
To interact with MongoDB directly, execute the following command to enter the MongoDB shell:
```bash
docker exec -it mongo-container-id mongosh
```
Replace `mongo-container-id` with the actual container ID or name of your MongoDB container.
6. Select the Database and View Tasks:
Use the MongoDB shell to switch to the `taskdb` database and list the tasks stored in the database:
```bash
use taskdb
db.tasks.find().pretty()
```
Notes:
• The frontend is served on [http://localhost:8080](http://localhost:8080), where you can interact with the app.
• The backend is running on [http://localhost:3000](http://localhost:3000) and handles tasks added to the database.
• MongoDB is used for storing tasks, and the connection is made between the backend and MongoDB through Docker networking.
