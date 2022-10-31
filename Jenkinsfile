pipeline{
    agent{
        label "nodejs"
    }

    environment{
        GREETING_NAMESPACE = 'issam-greetings'
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
            oc login --token=sha256~elxKs3VYJobU9ZdM665MVAkhorXOarxmpEUrS47FUls --server=https://api.eu46a.prod.ole.redhat.com:6443
            oc projects
            oc start-build greeting-console --follow --wait
            ''' 
            }
        }
    }
}
