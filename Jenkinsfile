pipeline{
    agent{
        label "nodejs"
    }

    environment{
        GREETING_NAMESPACE = "issam-greetings"
    }
    stages{
        stage("Install dependencies"){
            steps{
                sh "npm ci"
            }
        }

        stage("Check Style"){
            steps{
                sh "npm run lint"
            }
        }

        stage("Test"){
            steps{
                sh "npm test"
            }
        }

        // Add the Release stage here
        stage('Release') {
            steps {
            sh '''
            oc project "${env.GREETING_NAMESPACE}"
            oc start-build greeting-console --follow --wait
            ''' 
            }
        }
    }
}
