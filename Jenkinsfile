

pipeline{
    agent any
    environment{
        GITNAME='qwerqwsd'
        GITEMAIL='qwerqwsd@gmail.com'
        GITWEBADD='https://github.com/qwerqwsd/fast-code.git'
        GITSSHADD='git@github.com:qwerqwsd/deployment'
        GITCREDENTIAL='git_cre'
        ECR='278934099200.dkr.ecr.ap-northeast-2.amazonaws.com/fast'
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
                    sh "echo success"
                }
            }
        }
                        stage('imagebuild'){
            steps{

                slackSend (
                    channel: '#qwer',
                    color: '#FFFF00',
                    message: "STARTED: ${currentBuild.number}"
                )

                sh 'rm -f ~/.dockercfg ~/.docker/config.json || true'
                // sh "docker build -t ${DOCKERHUB}:${currentBuild.number} ."
                // sh "docker build -t ${DOCKERHUB}:latest ."
                // sh "docker build -t ${ECR}:${currentBuild.number} ."
                // sh "docker build -t ${ECR}:latest ."
                // currentBuild.number 젠킨스가 제공하는 빌드넘버 변수
                // oolralra/fast:<빌드넘버> 와 같은 이미지가 만들어질 예정.
                 
            }
            post{
                failure{
                    sh "echo failed"
                }
                success{
                    sh "echo success"
                }
            }
        }

        
                stage('docker image push'){
            steps{
                script{
                docker.withRegistry("https://278934099200.dkr.ecr.ap-northeast-2.amazonaws.com/fast", "ecr:ap-northeast-2:ecr") {
                def customImage = docker.build("${ECR}:${currentBuild.number}")
                customImage.push()
                }
                    }
            //      withDockerRegistry(credentialsId: DOCKERHUBCREDENTIAL, url: '') {
            //         sh "docker push ${DOCKERHUB}:${currentBuild.number}"
            //         sh "docker push ${DOCKERHUB}:latest"
            // }

                // sh "docker image rm -f ${DOCKERHUB}:${currentBuild.number}"
                // sh "docker image rm -f ${DOCKERHUB}:latest"
                sh "docker image rm -f ${ECR}:${currentBuild.number}"
                // sh "docker image rm -f ${ECR}:latest"
            }
            post{
                failure{
                    sh "echo failed"

                }
                success{
                    sh "echo imagebuild successed"
                }
            }
        }

                       stage('EKS manifest file update') {
            steps {
                git credentialsId: GITCREDENTIAL, url: GITSSHADD, branch: 'main'
                sh "git config --global user.email ${GITEMAIL}"
                sh "git config --global user.name ${GITNAME}"
                sh "sed -i 's@${ECR}:.*@${ECR}:${currentBuild.number}@g' fast.yml"

                sh "git add ."
                sh "git branch -M main"
                sh "git commit -m 'fixed tag ${currentBuild.number}'"
                sh "git remote remove origin"
                sh "git remote add origin ${GITSSHADD}"
                sh "git push origin main"
            }
            post {
                failure {
                    sh "echo manifest update failed"
                }
                success {
                    sh "echo manifest update success"
                }
            }
        }
       

    }
}

