Realiza los siguientes pasos:

1) Descarga Jenkins `docker pull jenkins:latest`{{execute}}

2) Levanta Jenkins.

`docker run -d -u root --name jenkins \
    -p 8080:8080 -p 50000:50000 \
    -v /root/jenkins:/var/jenkins_home \
    jenkins:latest`{{execute}}.

3) Abre Jenkins en una pestaña de la consola.

4) Investiga el Password de Jenkins.

`docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword`{{execute}}

5) Plugins: Instala únicamente el plugin de `Git Plugin`.

6) Admin: Crea un usuario administrador con los datos que gustes.

7) Listo!!!