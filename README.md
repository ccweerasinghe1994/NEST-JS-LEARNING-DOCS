# COMPLETE NEST JS COURSE

## Table of Contents

- [COMPLETE NEST JS COURSE](#complete-nest-js-course)
  - [Table of Contents](#table-of-contents)
  - [Controllers Routing Requests](#controllers-routing-requests)
    - [let's install nest js cli](#lets-install-nest-js-cli)
    - [let's create a new project](#lets-create-a-new-project)
    - [13 - Controllers](#13---controllers)
    - [14 - Resource Controller ✅](#14---resource-controller-)
    - [15 - Route Parameters ✅](#15---route-parameters-)
    - [16 - Request Body ✅](#16---request-body-)
    - [17 - Responses and Status Codes ✅](#17---responses-and-status-codes-)
    - [18 - Request Payload Data Transfer Objects ✅](#18---request-payload-data-transfer-objects-)
    - [19 - The Update Payload ✅](#19---the-update-payload-)
    - [20 - A Working API Example🔲](#20---a-working-api-example)
    - [🔲](#)
    - [🔲](#-1)
    - [🔲](#-2)
    - [🔲](#-3)
    - [🔲](#-4)
    - [🔲](#-5)
    - [🔲](#-6)
    - [🔲](#-7)
    - [🔲](#-8)
    - [🔲](#-9)
    - [🔲](#-10)
    - [🔲](#-11)
    - [🔲](#-12)
    - [🔲](#-13)
    - [🔲](#-14)
    - [🔲](#-15)
    - [🔲](#-16)
    - [🔲](#-17)

## Controllers Routing Requests

### let's install nest js cli

```bash
npm i -g @nestjs/cli
```

### let's create a new project

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

### 13 - Controllers

controller docs https://docs.nestjs.com/controllers

![Alt text](image-3.png)

![Alt text](<11 - Project-Structure-2x.png>)


![Alt text](<13 - Controllers-2x.png>)



let's create a controller

### 14 - Resource Controller ✅
![Alt text](<14 - Resource-Controller-2x.png>)

 Event, User, EventAttendee is a resource

databases are good candidates for resources

each resourse can have multiple operations.

![Alt text](image-4.png)
let's create a new controller

```bash
nest g controller events
```
![Alt text](image-5.png)


![Alt text](image-6.png)

try to keep the controller simple

![Alt text](image-7.png)

let's add the controller method
```ts
import { Controller, Get, Post, Patch, Delete } from '@nestjs/common';

@Controller('/event')
export class EventController {
  @Get()
  findAll() {}
  @Get()
  findOne() {}
  @Post()
  create() {}
  @Patch()
  update() {}
  @Delete()
  delete() {}
}

```
let's add the controller to the app module
```ts
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';
import { EventController } from './event.controller';

@Module({
  imports: [],
  controllers: [AppController, EventController],
  providers: [AppService],
})
export class AppModule {}

```

let's test the apis

```http
### GET EVENT
GET http://localhost:3000/event

### CREATE EVENT
POST http://localhost:3000/event

### DELETE EVENT

DELETE http://localhost:3000/event

### UPDATE EVENT
PATCH http://localhost:3000/event
```

output

![Alt text](image-8.png)

**SUMMERY**

![Alt text](image-9.png)












### 15 - Route Parameters ✅



![Alt text](<15 - Route-Parameters-2x.png>)

![Alt text](image-10.png)
```ts
import { Controller, Get, Post, Patch, Delete, Param } from '@nestjs/common';

@Controller('/event')
export class EventController {
  @Get()
  findAll() {}
  @Get(':id')
  findOne(@Param('id') id: string) {
    return id;
  }
  @Post()
  create() {}
  @Patch(':id')
  update(@Param('id') id: string) {
    return id;
  }
  @Delete(':id')
  delete(@Param('id') id: string) {
    return id;
  }
}

```

**SUMMERY**

![Alt text](image-11.png)
### 16 - Request Body ✅

let's add a body to the post request

![Alt text](image-12.png)


```ts
  @Post()
  create(@Body() body: any) {
    return body;
  }
```

let's test the api

```http
### CREATE EVENT
POST http://localhost:3000/event HTTP/1.1
content-type: application/json

{
  "name": "sample",
  "time": "Wed, 21 Oct 2015 18:27:50 GMT"
}

```

output
```json
{
  "name": "sample",
  "time": "Wed, 21 Oct 2015 18:27:50 GMT"
}
```

### 17 - Responses and Status Codes ✅
![Alt text](<17 - Responses-2x.png>)

code change

![Alt text](image-13.png)

code

```ts
import {
  Controller,
  Get,
  Post,
  Patch,
  Delete,
  Param,
  Body,
  HttpCode,
} from '@nestjs/common';

@Controller('/event')
export class EventController {
  @Get()
  findAll() {
    return [
      {
        id: 1,
        name: 'First event',
      },
      {
        id: 2,
        name: 'Second event',
      },
    ];
  }
  @Get(':id')
  findOne(@Param('id') id: string) {
    return id;
  }
  @Post()
  create(@Body() body: any) {
    return body;
  }
  @Patch(':id')
  update(@Param('id') id: string) {
    return id;
  }
  @Delete(':id')
  @HttpCode(204)
  delete(@Param('id') id: string) {
    return id;
  }
}

```

let's test the api

```http
### DELETE EVENT

DELETE http://localhost:3000/event/1 HTTP/1.1
```

![Alt text](image-14.png)

we can add status code to the response

```ts
  @Delete(':id')
  @HttpCode(204)
  delete(@Param('id') id: string) {
    return id;
  }
```

most used status codes

![Alt text](<17 - Status-Codes-2x.png>)

### 18 - Request Payload Data Transfer Objects ✅

let's create  a dto

```bash
export class CreateEventDto {
  name: string;
  when: string;
  address: string;
  description: string;
}
```

now we have access to the dto in the controller

```ts
  @Post()
  create(@Body() body: CreateEventDto) {
    console.log(body.description);
    console.log(body.name);
    console.log(body.address);
    console.log(body.when);
    return body;
  }
```


**Summery**
![Alt text](image-15.png)
### 19 - The Update Payload ✅

let's install @nestjs/mapped-types

```bash
npm i @nestjs/mapped-types
```
and create the update-event.dto.ts

```ts
import { PartialType } from '@nestjs/mapped-types';
import { CreateEventDto } from './create-event.dto';

export class UpdateEventDto extends PartialType(CreateEventDto) {}
```

and use it in the event.controller.ts

```ts
import {
  Controller,
  Get,
  Post,
  Patch,
  Delete,
  Param,
  Body,
  HttpCode,
} from '@nestjs/common';
import { CreateEventDto } from './create-event.dto';
import { UpdateEventDto } from './update-event.dto';

@Controller('/event')
export class EventController {
  @Get()
  findAll() {
    return [
      {
        id: 1,
        name: 'First event',
      },
      {
        id: 2,
        name: 'Second event',
      },
    ];
  }
  @Get(':id')
  findOne(@Param('id') id: string) {
    return id;
  }
  @Post()
  create(@Body() body: CreateEventDto) {
    console.log(body.description);
    console.log(body.name);
    console.log(body.address);
    console.log(body.when);
    return body;
  }
  @Patch(':id')
  update(@Param('id') id: string, @Body() body: UpdateEventDto) {
    console.log(body.description);
    console.log(body.name);
    console.log(body.address);
    console.log(body.when);
    return id;
  }
  @Delete(':id')
  @HttpCode(204)
  delete(@Param('id') id: string) {
    return id;
  }
}

```

![Alt text](image-16.png)

### 20 - A Working API Example🔲
![Alt text](<20 - Array.find-2x.png>)

spread operator https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax


### 🔲
### 🔲
### 🔲
### 🔲
### 🔲
### 🔲
### 🔲
### 🔲
### 🔲
### 🔲
### 🔲
### 🔲
### 🔲
### 🔲
### 🔲
### 🔲
### 🔲
### 🔲