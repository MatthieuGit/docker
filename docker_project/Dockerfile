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

