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