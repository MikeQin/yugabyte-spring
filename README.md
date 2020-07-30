# Yugabyte Spring

Build the REST API server (written using Spring code) as follows:

```
$ mvn -DskipTests package
```

Run the REST API server:

```
$ mvn spring-boot:run
```

**NOTE:** If you need to clean and rebuild the project, run the folowing command before rebuilding.

```
$ mvn clean
```

The REST server will run here: [`http://localhost:8080`](http://localhost:8080)

# Customizing

There are a number of options that can be customized in the properties file located here:
[`src/main/resources/application.properties`](src/main/resources/application.properties)

| Properties    | Description   | Default |
| ------------- | ------------- | ------- |
| `spring.datasource.url`  | The connection string. | `jdbc:postgresql://localhost:5433/postgres`  |
| `server.port`  | The port on which the REST API server should listen. | 8080 |
| `spring.datasource.username` | The username to connect to the database. | `postgres` |
| `spring.datasource.password` | The password to connect to the database. Leave blank for the password. | - |

# Data Injection

```
$ curl --data '{ "firstName" : "John", "lastName" : "Smith", "email" : "jsmith@yb.com" }' \
   -v -X POST -H 'Content-Type:application/json' http://localhost:8080/users

$ curl --data '{ "firstName" : "Tom", "lastName" : "Stewart", "email" : "tstewart@yb.com" }' \
   -v -X POST -H 'Content-Type:application/json' http://localhost:8080/users

curl \
  --data '{ "productName": "Notebook", "description": "200 page notebook", "price": 7.50 }' \
  -v -X POST -H 'Content-Type:application/json' http://localhost:8080/products

curl \
  --data '{ "productName": "Pencil", "description": "Mechanical pencil", "price": 2.50 }' \
  -v -X POST -H 'Content-Type:application/json' http://localhost:8080/products

curl \
  --data '{ "userId": "2", "products": [ { "productId": 1, "units": 2 } ] }' \
  -v -X POST -H 'Content-Type:application/json' http://localhost:8080/orders

curl \
  --data '{ "userId": "2", "products": [ { "productId": 1, "units": 2 }, { "productId": 2, "units": 4 } ] }' \
  -v -X POST -H 'Content-Type:application/json' http://localhost:8080/orders

```

# Query

## Using YSQL shell

```
yugabyte=# \d

yugabyte=# SELECT count(*) FROM users;
yugabyte=# SELECT count(*) FROM products;
yugabyte=# SELECT count(*) FROM orders;
yugabyte=# SELECT * FROM orderline;
```

## Using REST API

```
curl http://localhost:8080/users
curl http://localhost:8080/products
curl http://localhost:8080/orders
```