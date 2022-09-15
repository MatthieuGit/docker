# Docker project : Student list!

This page is a report about the Docker project produced as part of the **Eazytraining course**.

# Part 1 : Build and test

## Dockerfile

```
# --------------- DÉBUT COUCHE OS -------------------
FROM python:2.7-stretch
# --------------- FIN COUCHE OS ---------------------

#----------------- MÉTADONNÉES DE L'IMAGE------------
LABEL version="1.0"
MAINTAINER BAILLY Matthieu <matth.bailly@gmail.com>
#----------------- FIN METADONNEES DE L'IMAGE--------

# --------------- DÉBUT COUCHE PYTHON---------------
 RUN apt update -y && \
     apt-get install python-dev python3-dev libsasl2-dev python-dev libldap2-dev libssl-dev -y
 RUN pip install flask==1.1.2 flask_httpauth==4.1.0 flask_simpleldap python-dotenv==0.14.0

# --------------- FIN COUCHE PYTHON-----------------


#----------------DEBUT COUCHE GIT-------------------
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y git
#----------------FIN COUCHE GIT---------------------

#----------------OUVERTURE DU PORT------------------
EXPOSE 5000

#RECUPERATION DU PROJET DEPUIS GITHUB ET LE METTRE A L'EMPLACEMENT /data du container
RUN git clone https://github.com/diranetafen/student-list.git /data

#COPIE DU FICHIER student_age.py à la racine du container
COPY student_age.py /


#EXECUTION DE LA COMMANDE A FAIRE AU DEMARRAGE DU CONTAINER
CMD [ "python", "./student_age.py" ]
```

## BUILD IMAGE

```
docker build -t api .

-t for tag
```

## RUN CONTAINER

```
docker run -d -p 5000:5000 --name pozo -v data:/data  \
--mount type=bind,source="$(pwd)"/student_age.json,target=/student_age.json,readonly api
```
To run the container executed following command :
 -d : run container in background
 -p : define open port
 --name : container name
 -v : volume data will be created and mount in /data from the container
 --mount type : mount a specific file in the container

## CHECK LOGS
run following command:
```
docker logs CONTAINER_ID/CONTAINER NAME
```
>   Serving Flask app "student_age" (lazy loading)
>   Environment: production
 >   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
>   Debug mode: on
 >  Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
>   Restarting with stat
 >  Debugger is active!
>   Debugger PIN: 136-711-747

```
docker ps 
```
>CONTAINER ID   IMAGE     COMMAND                  CREATED       STATUS          PORTS                                       NAMES
5a91622d075c   api       "python ./student_ag…"   9 hours ago   Up 25 minutes   0.0.0.0:5000->5000/tcp, :::5000->5000/tcp   pozo

##  API CALL
```
curl -u toto:python -X GET http://192.168.4.40:5000/pozos/api/v1.0/get_student_ages
```

## Result

```
{
  "student_ages": {
    "alice": "12", 
    "bob": "13"
  }
}
```

