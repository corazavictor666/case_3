pipeline {
    
    agent any 

    stages {

        stage ('Source') {
            steps {
                git 'https://github.com/corazavictor666/'
            }
        }
    }

    stages {

        stage ('Build Image') {
            steps {
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
    }

    stages {

        stage ('Push image')
            steps {
                script {
                    docker.withRegistry ("") {
                        dockerImage.push ()
                    }
                }
            }
    }

    stage {

        stage ('Test')
            steps {
                script {
                    kubernetesDeploy (configs: "kubernetes.yaml", kubeconfigID "mykubeconfig")
                }
            }
    }

    
