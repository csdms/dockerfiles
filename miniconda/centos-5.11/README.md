CentOS 5.11 csdms-stack
=======================

Dockerfile for building the CSDMS software stack on CentOS 5.11.
CentOS 5.11 is *old* and not even supported anymore.

To build, copy the sources and run:

    $ docker build --rm -t <username>/csdms-stack .

To run,

    $ docker run -it <username>/csdms-stack

