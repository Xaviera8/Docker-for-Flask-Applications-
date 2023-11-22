# docker_flask_homework

## Part One: Dockerizing a Single Flask Application

### Set-up
Create a folder named part1 that contains the following:
1. requirements.txt file that contains flask.
2. app.py that should contain a flask application.
3. Docker file with the following code.

```
# Pulls the python base image
FROM python:3.9.18-bookworm
# Makes a new folder with the name app
WORKDIR /app
# This copies everything in our present working directory and appends it to the folder app 
COPY . /app
# Excutes the specified program
RUN pip install -r requirements.txt 
# Exposes the docker porgram to the desired port
EXPOSE 5000
# Executes specified commands via the command line
CMD ["python", "app.py"]
```
### Building the docker image
1. Using the terminal, change directories so that you are inside of the folder part1.
2. Use the command ```docker build -t xavier .```.
3. After the docker image is built, you can confirm its existence using the command ```docker images```.
4. Now that the docker image has been built, you can run the application with ```docker run -p 8005:5000 xavier```. This command conencts our local port 8005 with the VM's port 5000 and names the docker file xavier. 

### Deleting Docker Images
Docker images are saved and if you have two many images stored it can affect system memory.<br />To delete a docker image use ```docker system prune a f```.<br />The paramenter a will delete all images and f is used to "force". 

## Part Two: Multi-Container Setup with Docker Compose

### Set-up
1. Create a folder named Part2
2. Inside of Part2, create a docker-compose.yaml file, and two seperate folders named flask1 and flask2
3. Inside of each folder (flask1 and flask2), ensure there is a requirement.txt, app.py, and a docker file. The point of the exercise is to run multiple services at a time so ensure that the app.py files perform different functions.
4. In the docker file for each folder, include the following code.
```
# Pulls the python base image
FROM python:3.9.18-bookworm
# Makes a new folder with the name app
WORKDIR /app
# This copies everything in our present working directory and appends it to the folder app 
COPY . /app
# Excutes the specified program
RUN pip install -r requirements.txt 
# Exposes the docker porgram to the desired port
EXPOSE 5000
# Executes specified commands via the command line
CMD ["python", "app.py"]
```
5. Inside of the docker-compose file, input the following code. This code will dictate the local ports where our app.py services will run.
```
version: '3'
services:
  flask_app_1:
    build: ./flask1
    ports:
      - "5001:5000"
    volumes:
      - ./flask1:/app
  flask_app_2:
    build: ./flask2
    ports:
      - "5002:5000"
    volumes:
      - ./flask2:/app
```

### Building

1. Change directories to Part2
2. Run the command ```docker-compose up --build```.
3. Once the docker container has been built, you can preview the apps on different ports to ensure they are working as intended.
4. If you stop running the docker and need to start it again, use the command ```docker-compose up```.
5. To shut down a docker container, use the command ```docker-compose down```.
