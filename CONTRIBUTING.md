Contribution Guidelines
=======================

Each Dockerfile should contain a README
that includes the following:

* Version of the operating system that it
  was built and tested against.
* Instruction of building the Docker image.

For example:

    $ docker build --rm=true -t csdms/image .

* Instruction of running the Docker image.
  Including examples that use persistent data,
  port mapping, etc.
* Examples for testing and/or validating the
  functionality of the image.
* If yum is used during the build process, run
  a `yum clean` clean afterward to reduce the
  image size.
