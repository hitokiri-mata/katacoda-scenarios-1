## Agregar Nuevas Actividades

Editarás el archivo `Jenkinsfile` para agregar nuevas actividades al pipeline.

* Abre Github y navega hasta el archivo [`Jenkinsfile`](https://[[HOST_SUBDOMAIN]]-9876-[[KATACODA_HOST]].environments.katacoda.com/#jenkinsfile) del repositorio Pet Clinic.

* Para editar el archivo, has click en el **ícono de lapiz** en la parte superior derecha del archivo.

* Agrega las siguientes actividades al pipeline.

**Aprobación para iniciar el despliegue en el ambiente de Producción** 

Debajo del bloque `stage('End to End Tests'){..}`, agrega las siguientes líneas:

<pre class="file" data-target="clipboard">
stage('Decide Deploy to Prod'){
    when {
        branch 'master'
    }
    agent none
    steps {
        input message: 'Deploy to Prod?'
    }            
}
</pre>

**Desplegar en Producción** 

* El despliegue consisten en detener el contenedor anterior y ejecutar la nueva versión.

* Debajo del bloque `stage('Decide Deploy to Test'){..}`, agrega las siguientes líneas:

    <pre class="file" data-target="clipboard">
    stage('Deploy Prod'){
        when {
            branch 'master'
        }
        agent any
        steps {
            sh '''
                for runName in `docker ps | grep "alpine-petclinic-prod" | awk '{print $1}'`
                do
                    if [ "$runName" != "" ]
                    then
                        docker stop $runName
                    fi
                done
                docker run --name alpine-petclinic-prod --rm -d -p 9968:8080 $TAG_NAME
            '''
        }
    }   
    </pre>

## Probar el pipeline

* En la sección **Commit changes**, ingresa un comentario, por ejemplo `Pipeline: producción`{{copy}}

* Realiza commit del código en la misma rama `master`.