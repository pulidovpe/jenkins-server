# jenkins-server
Jenkins-server-custom

# Que es Jenkins y que tan importante es para un Devops.

Jenkins es un sistema que nos permite deplegar componentes de forma manual, automatica o semi automatica contemplando por ejemplo los siguientes escenarios.

- Programar acciones en el tiempo
- Activacion por script 
- Cambios en un repositorio 

Para un Devops poder contar con una herramienta como Jenkins es vital para centralizar todas las tareas programadas o manuales en un solo sitio, contando con un panel donde podremos ver el estado de cada una y mejorarla.

# Objetivo 

  En este repositorio encontraremos una copia del repositorio oficial de Jenkins donde personalizaremos la instalacion del mismo para poder reutilizar la misma a futura y aplicar mejoras segun las necesidades.

# Otras Herramientas y lenguajes que utilizara un Devops.

Jenkins no hace magia, necesita de otras herramientas o lenguajes que utilizan en la empresa para poder trabajar como puede ser :

- Github, Gitlab, Nexus
- Ansible, Terraform
- Vault, Ldap
- Conexiones a recursos cloud
- Python , bash, grooby

# Fuente de de Jenkins: 
    https://hub.docker.com/r/jenkins/jenkins/

# Codigo de Jenkins: 
    https://github.com/jenkinsci/docker

# Mejoras a realizar en la imagen

En el archivo Dockerfile realizaremos las mejoras oportunas para ahorrarnos tiempo, si tenemos que repetir el proceso.

```
RUN apt-get update && apt-get upgrade -y && apt-get install -y git curl && curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | bash && apt-get install -y git-lfs && git lfs install && rm -rf /var/lib/apt/lists/*
RUN apt-get update
RUN apt-get install -y  python3
RUN apt-get install -y  python-pip python3-pip
RUN apt-get install -y virtualenv
RUN pip install  cryptography==2.7
RUN pip3 install  cryptography==2.7
RUN apt-get install -y software-properties-common
RUN apt-get install -y awscli
RUN pip3 install ansible==2.5.0
RUN pip3 install hvac
RUN pip3 install boto
RUN echo "root:root" | chpasswd
```


# Creacion de la imagen con las modificaciones 
```
docker build -t "jenkins:v3" .
```

# Desplegar un contenedor con Jenkins server con la imagen previamente desplegada

Ejemplos de como desplegar dos servidores con configuraciones separadas.
```
docker run -d -v jenkins_home:/var/jenkins_home -p 8080:8080 -p 50000:50000 jenkins:v3
docker run -d -v jenkins_home_v4:/var/jenkins_home -p 8080:8080 -p 50000:50000 jenkins:v4
```

* Recordemos los volumenes nos mantienen los ficheros que contienen de forma persistente.
docker volume ls   --->  para listar los volumenes 
docker volume inspect my-vol   --> listar caracteristicas de cada volumen 
[
    {
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/var/lib/docker/volumes/my-vol/_data",
        "Name": "my-vol",
        "Options": {},
        "Scope": "local"
    }
]


# Accedemos por http

Accedemos via http al contenedor recien instalado y por unica vez nos pedira la contraseña 
que se encuentra en: 
```
cat /var/lib/jenkins/secrets/initialAdminPassword
```

## Creamos el usuario admin

Completamos formulario con datos del nuevo usuario 

# Accedemos al contenedor 

```
docker exec -it c088 /bin/bash
```


# ----------------------------------------------------
# Administracion por terminal 
# Cambiamos de usuario para mejoras sobre 
su root  --> root
# apt install 
apt install net-tools









