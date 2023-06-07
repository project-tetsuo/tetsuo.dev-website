# Tetsuo Architecture

When writing an architecture section it's always fun. Depending on your point of view you will want to see different things. I have tried y best to cover the different bases that I can think of so far, but this is an evolving document.

If you want to change it please open a pull request.

## Infrastructure Architecture

## Software Architecture

The software architecture of Tetsuo is largely based on a few things:
- Be simple
- Use native NGINX Unit functionality where possible.
- Have a minimum of services to interact with that will deploy my codebase.

![Tetsuo-overview](/images/Tetsuo-overview.jpg)

The individual services are desribed below.

## Services

There is no single over riding language or framework that is used as part of our architecture. The idea is that you should use the language that makes the most sense for the service in question. 

We currently have two services - with some more to follow - these are described in detail below.

### Git Service

Language: Golang

Purpose:
The purpose of this service is to receive a request and pull down code from a git repository into a standardised location on the Tetsuo server. This will allow a developer to simply upload their code and then trigger the git service to pull it down onto the Tetsuo server. This is the first part of deployment. **Get the code there**.

The service currently accepts some values as part of a post request. 

URL - This represents the URL of the git repository that your code lives in. This is the full http://somegitrepo.com string. That is, the string needs to include the http:// component as well. We figured more people will simply cut and paste this value so including it would make sense.

BRANCH - This is the branch of the code that you would like to pull. This absolutely needs to be included. There is no default given. There is no assumption that "main" is the branch that you would like to pull on our behalf. It is a mandatory field.

```Bash
curl -s -X POST -H "Content-Type: application/json" http://**TETSUO-SERVER**/pull -d '{"url":"https://github.com/codecowboydotio/swapi-json-server", "branch":"dev"}'
```
![git_api](/images/tetsuo-1-2.jpg)

Modules:
**fmt** - primarily used for printing outputs for debugging during development.

**os** - Used for printing status of git clone (can probably be removed)

**path** - Used for expanding the target path on the application server

**net/http** - Netwokr library

**net/url** - Used to parse the incoming target URL

**github.com/gin-gonic/gin** - Gin for REST API 

**github.com/go-git/go-git/v5** - go-git for interacting with GIT

**github.com/swaggo/files** - Used to generate swagger docs

**github.com/gin-contrib/cors** - Unit does not currently support CORS natively so this is a hack to allow CORS requests for each individual service.

**unit.nginx.org/go** - For golang applictions this is the unit router

Notes: At the moment, the target directory on the unit server is hard coded. This is something we have thought about a lot. Given the ultimate aim is a SaaS like service, this has been debated a lot. There is an inherent balance between opinionated and configurable. 

### Config Service

Language: Python

Purpose: 
The purpose of the config API is to both update the configuration, but to also 
