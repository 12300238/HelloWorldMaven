pipeline {
    agent any
    
    stages {
        stage('###################  Build  #########################') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/12300238/HelloWorldMaven.git'
                // Run Maven on a Unix agent.
                sh "mvn clean install"
            }
            post {
                success {
                    script {
                        sh "git tag -a v2.${BUILD_NUMBER} -m 'Great build' || true"
                        
                        // Pousser le tag avec credentials
                        withCredentials([usernamePassword(
                            credentialsId: '4aa942a6-ae93-413c-afc5-3cfb0029a962',
                            usernameVariable: 'GIT_USERNAME',
                            passwordVariable: 'GIT_PASSWORD'
                        )]) {
                            sh """
                                git config user.email "jenkins@example.com"
                                git config user.name "Jenkins"
                                git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/12300238/HelloWorldMaven.git --tags
                            """
                        }
                    }
                }
            }
        }
    }
}
