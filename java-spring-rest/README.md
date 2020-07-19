# java-spring-rest
> Tutorial used can be found [here](https://spring.io/guides/tutorials/rest/)

I initially used this tutorial to introduce me into the [Spring Framework](spring.io), Java's popular application development framework. For anyone
trying to learn this framework, I highly recommend using this tutorial. Personally, it also taught me more about REST principles and helped give me 
a basic Java refresher.

## Using this project
### Launching application...
#### ... with the command line
Get started by cloning this repo and changing into the subproject's directory (`./java-spring-rest`).

```
git clone https://github.com/mikebarrameda/tutorials
cd tutorials/java-spring-rest
```
This project comes with maven pre-installed, so you don't have to download it yourself.
```
./mvnw clean spring-boot:run
```


#### ... with an IDE
Get started by cloning this repo and opening the subproject (`./java-spring-rest`) in your favorite Java IDE of choice. I used IntelliJ Community Edition.
Right click on `src/main/java/payroll/PayrollApplication.java` and click `RunApplication`. This will differ from IDE to IDE.

### Test out the APIs using curl
#### Fetch all employees
```
curl -v localhost:8080/employees | json_pp
```
```
> GET /employees HTTP/1.1
> Host: localhost:8080
> User-Agent: curl/7.64.1
> Accept: */*
>
< HTTP/1.1 200
< Content-Type: application/hal+json
< Transfer-Encoding: chunked
< Date: Sun, 19 Jul 2020 15:08:40 GMT
<
{ [410 bytes data]
100   403    0   403    0     0  31000      0 --:--:-- --:--:-- --:--:-- 31000
* Connection #0 to host localhost left intact
* Closing connection 0
{
   "_embedded" : {
      "employeeList" : [
         {
            "role" : "burglar",
            "lastName" : "Baggins",
            "firstName" : "Bilbo",
            "name" : "Bilbo Baggins",
            "_links" : {
               "employees" : {
                  "href" : "http://localhost:8080/employees"
               }
            },
            "id" : 1
         },
         {
            "id" : 2,
            "_links" : {
               "employees" : {
                  "href" : "http://localhost:8080/employees"
               }
            },
            "name" : "Frodo Baggins",
            "firstName" : "Frodo",
            "lastName" : "Baggins",
            "role" : "thief"
         }
      ]
   },
   "_links" : {
      "self" : {
         "href" : "http://localhost:8080/employees"
      }
   }
}
```
#### Fetch one employee
```
curl -v localhost:8080/employees/1 | json_pp
```
```
> GET /employees/1 HTTP/1.1
> Host: localhost:8080
> User-Agent: curl/7.64.1
> Accept: */*
>
< HTTP/1.1 200
< Content-Type: application/hal+json
< Transfer-Encoding: chunked
< Date: Sun, 19 Jul 2020 15:09:26 GMT
<
{ [161 bytes data]
100   155    0   155    0     0   4843      0 --:--:-- --:--:-- --:--:--  4843
* Connection #0 to host localhost left intact
* Closing connection 0
{
   "firstName" : "Bilbo",
   "name" : "Bilbo Baggins",
   "lastName" : "Baggins",
   "role" : "burglar",
   "_links" : {
      "employees" : {
         "href" : "http://localhost:8080/employees"
      }
   },
   "id" : 1
}
```
#### Create a new employee
```
curl -v -X POST localhost:8080/employees -H 'Content-type:application/json' -d '{"firstName": "Samwise", "lastName": "Gamgee", "role": "gardener"}' | json_pp
```
```
> POST /employees HTTP/1.1
> Host: localhost:8080
> User-Agent: curl/7.64.1
> Accept: */*
> Content-type:application/json
> Content-Length: 66
>
} [66 bytes data]
* upload completely sent off: 66 out of 66 bytes
< HTTP/1.1 201
< Location: http://localhost:8080/employees/5
< Content-Type: application/hal+json
< Transfer-Encoding: chunked
< Date: Sun, 19 Jul 2020 15:34:44 GMT
<
{ [216 bytes data]
100   276    0   210  100    66    349    109 --:--:-- --:--:-- --:--:--   460
* Connection #0 to host localhost left intact
* Closing connection 0
{
   "lastName" : "Gamgee",
   "name" : "Samwise Gamgee",
   "firstName" : "Samwise",
   "_links" : {
      "self" : {
         "href" : "http://localhost:8080/employees/5"
      },
      "employees" : {
         "href" : "http://localhost:8080/employees"
      }
   },
   "id" : 5,
   "role" : "gardener"
}
```
#### Modify an existing employee
```
curl -v -X PUT localhost:8080/employees/5 -H 'Content-type:application/json' -d '{"firstName": "Sam","lastName": "Gamgee", "role": "ring bearer"}' | json_pp
```
```
> PUT /employees/5 HTTP/1.1
> Host: localhost:8080
> User-Agent: curl/7.64.1
> Accept: */*
> Content-type:application/json
> Content-Length: 64
>
} [64 bytes data]
* upload completely sent off: 64 out of 64 bytes
< HTTP/1.1 201
< Location: http://localhost:8080/employees/5
< Content-Type: application/hal+json
< Transfer-Encoding: chunked
< Date: Sun, 19 Jul 2020 15:35:01 GMT
<
{ [216 bytes data]
100   269    0   205  100    64   2157    673 --:--:-- --:--:-- --:--:--  2831
* Connection #0 to host localhost left intact
* Closing connection 0
{
   "lastName" : "Gamgee",
   "firstName" : "Sam",
   "_links" : {
      "employees" : {
         "href" : "http://localhost:8080/employees"
      },
      "self" : {
         "href" : "http://localhost:8080/employees/5"
      }
   },
   "id" : 5,
   "role" : "ring bearer",
   "name" : "Sam Gamgee"
}
```
#### Fetch all orders
```
curl -v http://localhost:8080/orders
```
```
> GET /orders HTTP/1.1
> Host: localhost:8080
> User-Agent: curl/7.64.1
> Accept: */*
>
< HTTP/1.1 200
< Content-Type: application/hal+json
< Transfer-Encoding: chunked
< Date: Sun, 19 Jul 2020 15:29:20 GMT
<
{ [545 bytes data]
100   538    0   538    0     0  28315      0 --:--:-- --:--:-- --:--:-- 28315
* Connection #0 to host localhost left intact
* Closing connection 0
{
   "_links" : {
      "self" : {
         "href" : "http://localhost:8080/orders"
      }
   },
   "_embedded" : {
      "orderList" : [
         {
            "description" : "MacBook Pro",
            "_links" : {
               "self" : {
                  "href" : "http://localhost:8080/orders/3"
               },
               "orders" : {
                  "href" : "http://localhost:8080/orders"
               }
            },
            "id" : 3,
            "status" : "COMPLETED"
         },
         {
            "id" : 4,
            "status" : "IN_PROGRESS",
            "description" : "iPhone",
            "_links" : {
               "self" : {
                  "href" : "http://localhost:8080/orders/4"
               },
               "cancel" : {
                  "href" : "http://localhost:8080/orders/4/cancel"
               },
               "complete" : {
                  "href" : "http://localhost:8080/orders/4/complete"
               },
               "orders" : {
                  "href" : "http://localhost:8080/orders"
               }
            }
         }
      ]
   }
}
```
#### Cancel one order
```
curl -v -X DELETE http://localhost:8080/orders/4/cancel
```
```
> DELETE /orders/4/cancel HTTP/1.1
> Host: localhost:8080
> User-Agent: curl/7.64.1
> Accept: */*
>
< HTTP/1.1 200
< Content-Type: application/hal+json
< Transfer-Encoding: chunked
< Date: Sun, 19 Jul 2020 15:31:36 GMT
<
{ [167 bytes data]
100   161    0   161    0     0  13416      0 --:--:-- --:--:-- --:--:-- 13416
* Connection #0 to host localhost left intact
* Closing connection 0
{
   "description" : "iPhone",
   "id" : 4,
   "status" : "CANCELLED",
   "_links" : {
      "self" : {
         "href" : "http://localhost:8080/orders/4"
      },
      "orders" : {
         "href" : "http://localhost:8080/orders"
      }
   }
}
```
## Tutorial Troubleshooting
#### ./mvnw did not successfully start the application
The `./mvnw` file didn't actually work out of the box. I had to run
```
mvn -N io.takari:maven:wrapper
```
to install the wrapper configurations so it could actually work.
#### EmployeeModelAssembler missing self link
I had to add
```
linkTo(methodOn(EmployeeController.class).one(employee.getId())).withSelfRel()
```
to line 15 of `src/main/java/payroll/EmployeeModelAssembler.java`.
