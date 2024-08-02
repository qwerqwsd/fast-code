pipeline{
    agent any

    stages {

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