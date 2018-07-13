# registry: List of Docker containers for LSP pipelines

Full list on Dockerhub: https://hub.docker.com/u/datarail/

Current containers:
  * concat - "Hello World" example demonstrating the usage of Docker and docker-compose. [[GitHub](https://github.com/datarail/concat-docker)]
  * pamsig -  Clusters segmented CyCIF data using Partitioning Around Medoids (PAM) and produces signatures that define each cluster. [[GitHub](https://github.com/datarail/cscwg)][[Example data](http://s3.amazonaws.com/datarail-example-data/pamsig/CyCIF1.csv)]
  
## Instructions for Developers

### Prepare

  1. Set up your code to be executable from command line.
  2. Modify your code to read all input from `/input/` and write all output to `/output/`
  3. Have your code read method-specific parameter settings from `/config/<container name>.yml`

### Package

  1. Put together a Dockerfile that lists all the necessary dependencies for containerizing your code. See examples for [Python](https://github.com/datarail/concat-docker/blob/master/Dockerfile) and [R](https://github.com/datarail/cscwg/blob/master/pamsig/Dockerfile).
  2. Build your container by running `docker build -t datarail/<container name>:v1 .` (Replace `<container name>` with the name of your container and `v1` with the version number).
  3. Verify locally that your container runs as expected by executing `docker run -v <path to config>:/config -v <path to data>:/input -v <path to results>:/output datarail/<container name>:v1`

### Deploy

  1. Upload your code to a GitHub repository. Include an example config file, as well as a README that describes the expected parameter fields.
  2. Create a DockerHub account. Contact Jeremy, Douglas or Artem to be added to the datarail group.
  3. Push your container image to DockerHub by running
  ```
  docker login
  docker push datarail/<container name>:v1
  ```
  4. Send an e-mail to Artem with a one-paragraph description of your method and a link to your GitHub repo.

### Exemplify

  It is strongly recommended to create an exemplar dataset to be used with your container. Currently, LSP hosts exemplar data for Datarail pipelines in AWS S3 buckets. To upload your data, post in the @aws Slack channel requesting to be added to our AWS organization. After getting access, upload your data to `datarail-example-data/<container name>/`.
