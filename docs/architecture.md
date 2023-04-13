# Tetsuo Architecture

When writing an architecture section it's always fun. Depending on your point of view you will want to see different things. I have tried y best to cover the different bases that I can think of so far, but this is an evolving document.

If you want to change it please open a pull request.

## Infrastructure Architecture

## Software Architecture

The software architecture of Tetsuo is largely based on a few things:
- Be simple
- Use native NGINX Unit functionality where possible.
- Have a minimum of services to interact with that will deploy my codebase.

The individual services are desribed below.

## Services

There is no single over riding language or framework that is used as part of our architecture. The idea is that you should use the language that makes the most sense for the service in question. 

We currently have two services - with some more to follow - these are described in detail below.

### Git Service

Language: Golang

Purpose:
The purpose of this service is to receive a request and pull down code from a git repository into a standardised location on the Tetsuo server. This will allow a developer to simply upload their code and then trigger the git service to pull it down onto the Tetsuo server. This is the first part of deployment. **Get the code there**.

The service currently accepts some values as part of a post request. 



Modules:

### Config Service



