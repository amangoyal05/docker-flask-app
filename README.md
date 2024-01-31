# docker-flask-app
This is a simple Flask app that says hello from Docker's, Flask's and my side. The flask code is written in the app.py file.<br>

After that, create a Dockerfile which consists of all the configurations.<br>
```html
FROM python:latest sets the base image for the Docker image.

WORKDIR /app sets the working directory inside the container to '/app/.

COPY . /app copies all the apps from the current folder to '/app' working directory.

RUN pip install --trusted-host pypi.python.org -r requirements.txt installs Python dependencies specified in the 'requirements.txt' file using the 'pip' package manager. The '--trusted-host' flag is used to indicate the trusted host for downloading packages, i.e.pypi.python.org

EXPOSE 5000 informs Docker that the container will listen on port 5000 at runtime.

ENV NAME World sets an environment variable named 'NAME' with the value 'World'. This variable can be accessed by applications running inside the container.

CMD ["python", "app.py"] specifies the default command to run when the container starts. Here, it launches the Python script "app.py".
```
Once the Dockerfile is made, we need to build the image for the app using the following command - <br>
```sh
docker build -t tag-name .
```
Then we run the Docker container using the following command - 
```sh
docker run -p 4000:5000 tag-name
```
'-p 4000:5000' flag maps port 5000 inside the container to port 4000 on the host machine.

To expose the local server to the internet for testing, open a new terminal window and run the following command -
```sh
ngrok http 4000
```
This will provide you with a random domain link which you can use to view your application.

Now, create a repository on docker hub. Let's call it test.
Open the CLI and perform the following commands -

```sh
docker tag tag-name your-docker-username/test:latest
```
The above command tags the existing Docker image named 'app' with a new name 'your-docker-username/test' and tag it as 'latest'. This is a necessary step before pushing the image to a Docker registry like Docker Hub. It helps in organizing and identifying the Docker images with meaningful names and tags.

Then we push the image to the repository using - 

```sh
docker push your-docker-username/test:latest
```

This is how we can push an image to Docker Hub.
