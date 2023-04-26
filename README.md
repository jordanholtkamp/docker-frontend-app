# Docker Frontend React App

This is a project displaying some work I did for a minimal React app that utilizes Docker to create images for develop, testing, and production environments.

To build the image once you have the repository cloned and are in the project dir, you can do one of two things:
1. Run `docker-compose -f docker-compose-dev.yml up --build`
2. Run `docker build -f Dockerfile.dev .` and then the Docker CLI will return an image created on build and you can copy and paste it into the next command: `docker run #{image_id}`

Either of these approaches will start up your development environement by installing all of your dependencies in a node:alpine base image and starting your dev server on port 3000 on your local machine.

## Other tech utilized
This project uses Travis CI to leverage CI/CD for a production environment by hooking into AWS Elastic Beanstalk. The app also utilizes an nginx base imeage from Docker as a production-grade server to host my production application on AWS. We also utilize docker volumes to have live updates on the code into our dev environment so as to not need for a new docker build each time we make a change to source code.

## Running the Test Suite
To run the test suite you can simply override the default `Dockerfile.dev` command by adding a new one at the end of your `docker run` command. After you have your built image, run: `docker run -it #{image_id} npm run test`. Remember that to build the image in the dev environment, you have to build the `Dockerfile.dev` file. The regular `Dockerfile` is meant to be built only for the production environment.
