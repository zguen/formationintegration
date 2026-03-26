pipeline {
    agent { label 'noeud-test' }

    tools {
        maven 'M3'
    }

    environment {
        IMG="formationintegration-guillaume:${env.BUILD_ID}"
        CT_NAME="formationintegration-guillaume-container"
    }

    stages {
        stage('Compilation') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage ('Buil docker image') {
            steps {
                sh "docker build -t ${IMG} ."
            }
        }

        stage ('Deploiement') {
            steps {
                sh "docker stop ${CT_NAME) ||  true"
                sh "docker rm ${CT_NAME) ||  true"
                sh "docker run -d --name  ${CT_NAME} ${IMG}"
            }
        }
    }

    post {
        success {
            echo "Ca a fonctionné"
            sh "docker ps | grep ${CT_NAME}"
        }
    }
}
 
