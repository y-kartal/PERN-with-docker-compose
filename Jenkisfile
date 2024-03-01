pipeline{
    agent any
    tools {
           docker 'docker'            
    }

    stages { 
        stage('Deploy the App') {
            steps {
                echo 'Deploy the App'
                sh 'ls -l'
                sh 'docker --version'
                script {
                    dockerComposeBuild(
                        composeFile: 'docker-compose.yaml')
                }        
             }
        }

    

        stage('Destroy the infrastructure'){
            steps{
                timeout(time:5, unit:'DAYS'){
                    input message:'Approve terminate'
                }
                script {
                    dockerComposeDown(
                        composeFile: 'docker-compose.yaml')
                } 
            }
        }
    }

    post {
        success {
        script {
        slackSend channel: '#class-chat', color: '#439FE0', message: ' :100: Project-207 with jenkins :100:', teamDomain: 'devops15tr', tokenCredentialId: 'jenkins-slack'
            }
    }
    }  

}
