pipeline{
    agent any

    stages {
        environment{
            GITNAME='qwerqwsd'
            GITMAIL='qwerqwsd@gmail.com'
            GITWEBADD='https://github.com/qwerqwsd/fast-code.git'
            GITSSHADD='git@github.com:qwerqwsd/fast-code.git'
            GITCREDENTIAL='gir_cre'
            DOCKERHUB='qwerqwsd/fast'
            DOCKERHUBCREDENTIAL='docker_cre'
        }
        stage(start){
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