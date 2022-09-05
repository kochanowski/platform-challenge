## 1. Overview

All 3 services of `platform-challenge` are configured with [docker-compose](https://docs.docker.com/compose/install/) with Dockerfiles for each service and [Treafik](https://doc.traefik.io/traefik/) in front of them. 

## 2. Configuration

* Please put into your `/etc/hosts` the following line to get proper DNS working:
`127.0.0.1       platform` 

* Each service is configured via environment variables:
  `auth-api/code/local_env`
  `core-api/code/local_env`
  `psp-connector/code/local_env`

## 3. Running on the local machine
* To run the stack in background run `docker-compose up -d`
* Traefik dashboard is available at `http://localhost:8080/`
* To rebuild the image run `docker-compose up --force-recreate --build`
* To run services with `DEBUG` mode for each service uncomment the following lines in `docker-compose` file:
```
    environment:
      - FLASK_ENV=development    
```
## 4. Examples
```
$ http POST http://platform/auth/token username=alice password=password
HTTP/1.1 200 OK
Content-Length: 179
Content-Type: application/json
Date: Sun, 04 Sep 2022 17:34:12 GMT
Server: hypercorn-h11

{
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyX2lkIjoxLCJ1c2VybmFtZSI6ImFsaWNlIiwiZW5hYmxlZCI6dHJ1ZSwiZXhwIjoxNjYyMzEyODgyfQ.uhb1HM-M9UM8BCWtDRRgPYR6njBGEByLHQwxmoSqdz0"
}
```
```
$ http POST http://platform/transaction amount=100 currency=USD   token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyX2lkIjoxLCJ1c2VybmFtZSI6ImFsaWNlIiwiZW5hYmxlZCI6dHJ1ZSwiZXhwIjoxNjYyMzEyODgyfQ.uhb1HM-M9UM8BCWtDRRgPYR6njBGEByLHQwxmoSqdz0
HTTP/1.1 200 OK
Content-Length: 44
Content-Type: application/json
Date: Sun, 04 Sep 2022 17:34:36 GMT
Server: Werkzeug/2.0.2 Python/3.9.7

{
    "amount": 100,
    "currency": "USD",
    "user_id": 1
}
```
