pipeline{
    agent any
    environment{
        GITNAME='qwerqwsd'
        GITMAIL='qwerqwsd@gmail.com'
        GITWEBADD='https://github.com/qwerqwsd/fast-code.git'
        GITSSHADD='git@github.com:qwerqwsd/fast-code.git'
        GITCREDENTIAL='gir_cre'
        DOCKERHUB='qwerqwsd/fast'
        DOCKERHUBCREDENTIAL='docker_cre'
    }
    stages {

        stage('Checkout Github'){
            steps{
                checkout([$class: 'GitSCM',branches: [[name: '*/main']], extensions: [],
                userRemoteConfigs: [[credentialsId: GITCREDENTIAL, url: GITWEBADD]]])
            }
            post{
                failure{
                    sh "echo failed"
                }
                success{
                    sh "echo failsed"
                }
            }
        }
                stage('docker image build'){
            steps{
                 withDockerRegistry(credentialsId: DOCKERHUBCREDENTIAL, url: '') {
                    sh "docker push ${DOCKERHUB}:${currentBuild.number}"
                    sh "docker push ${DOCKERHUB}:latest"
            }
            post{
                failure{
                    sh "echo imagebuild failed"
                }
                success{
                    sh "echo imagebuild successed"
                }
            }
        }
                stage('start2'){
            steps{
                sh "echo hello Jenkins!!"
                 
            }
            post{
                failure{
                    sh "echo failed"
                }
                success{
                    sh "echo failed"
                }
            }
        }
                stage('start3'){
            steps{
                sh "echo hello Jenkins!!"
                 
            }
            post{
                failure{
                    sh "echo failed"
                }
                success{
                    sh "echo failed"
                }
            }
        }
    }
    
}