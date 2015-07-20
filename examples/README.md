# Introduction

This is a suggested order for moving through the examples of the Nulecule specification using the [Atomicapp reference implementation](https://github.com/projectatomic/atomicapp).  Readers of this document should have read the [Nulecule README](https://github.com/projectatomic/nulecule/README.md) and understand docker containers and have done the following:

- built a container from a Dockerfile
- run a container using `docker run` from the command line
- accessed a network service running in a docker container

To follow these examples, the following needs to be installed:

- [docker](https://docs.docker.com/)
- [kubernetes](http://kubernetes.io/)
- [atomic](https://github.com/projectatomic/atomic)

Installation directions are generally outside of the scope of this document and can be found in the public repositories or in your operating system's documenation set.  Note: If you need to install Kubernetes, the easiest way to get it running for demo purposes is to use the containerized installation instructions at https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/getting-started-guides/docker.md in the Kubernetes GitHub repository.

## helloapache

Goal: Launch an application that has been specified via Nulecule

The simplest example in programming is 'hello world', the analogous example for Nulecule is 'helloapache'.  This example illustrates how to launch a single container application that consists of an unconfiguredApache webserver running in a CentOS container.

Suggested Items to Focus On:

- Review the answers.conf file and compare it to the Nulecule file.  Notice how your answers refer to the `graph->params` section.  
- Review the files in the `artifacts` directory and see how the params are used in the commands and/or configuration files.
- Change the provider from kubernetes to native docker.

## mariadb-fedora-atomicapp

Goal: Launch an application that needs application specific configuration that is specified via Nulecule

Much like helloapache, this example only launches a single container.  However, the container is now a fedora container with a mariadb server instead of a CentOS container with an Apache webserver.  Mariadb requires configuration before it is useful, such as a username/password combination.  This is all specified via the Nulecule file.

Suggested Items to Focus On:

- Review how the "db_user", "db_pass", and "db_name" parameters are used in the provider files.  The mariadb container image has been configured to allow environment variables to be used to provide the initial setup.
- Notice that the artifacts for the providers are now stored in a directory called "graph" illustrating the flexibilty of the specification to support file naming and directory structure schemes that make the most sense for the application.
- The kubernetes provider has been expanded to set up a service.
- Be sure to run Option #1 and see how the parameters that do not have default values are prompted for.

## mariadb-centos7-atomicapp

Goal: Show same Nulecule running a different os-based image

This example essentially duplicates mariadb-fedora-atomicapp.  The only difference is that mariadb is now running on CentOS instead of on Fedora.

Suggested Items to Focus On:

- Notice that in this example, the image is hardcoded in the artifact files.
- Notice that this example uses the same parameters as mariadb-fedora-atomicapp but applies this differently because the images are structured differently.

## redis-centos7-atomicapp

Goal: Show a nulecule composed of two containers.

This example brings up a redis-master and 2 redis-slaves.  They all launch from the same image but with different configuration.

Suggested Items to Focus On:
- Notice how the master's port is passed to the slaves.
- Notice how the number of slaves is managed by the orchestration provider.

## guestbook-go

- uses redis-centos7-atomicapp

## skydns-atomicapp

## wordpress-centos7-atomicapp

- uses mysql-centos7-atomicapp and skydns-atomicapp
- for this be sure to show moving across providers here and how the included apps just work
- also swap out the mariadb
