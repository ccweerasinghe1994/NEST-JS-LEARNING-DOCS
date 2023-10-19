# COMPLETE NEST JS COURSE

## Table of Contents

- [COMPLETE NEST JS COURSE](#complete-nest-js-course)
  - [Table of Contents](#table-of-contents)
  - [Controllers Routing Requests](#controllers-routing-requests)
  - [let's install nest js cli](#lets-install-nest-js-cli)
  - [let's create a new project](#lets-create-a-new-project)

## Controllers Routing Requests

## let's install nest js cli

```bash
npm i -g @nestjs/cli
```

## let's create a new project

```bash
nest new project-name
```

![Alt text](image-2.png)

let's create http file for the api calls

```bash
touch API.http
```
add the default route to the http file

```http
GET http://localhost:3000 HTTP/1.1
```


![Alt text](image.png)

nest js cli link : https://docs.nestjs.com/cli/usages

let's create a sample controller method

![Alt text](image-1.png)

```http
GET http://localhost:3000/bye HTTP/1.1
```

summery 

![Alt text](image-3.png)

![Alt text](<11 - Project-Structure-2x.png>)


![Alt text](<13 - Controllers-2x.png>)

![Alt text](<14 - Resource-Controller-2x.png>)


let's create a controller

