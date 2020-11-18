pipeline {
    agent any
    tools { 
        maven 'Jenkins Maven' 
    }

    stages {
        stage('Build') {
            steps {
                //snDevOpsStep()
                sh '''
                    mvn --version
                '''
                sh 'mvn compile'   
            }
        }
        
        stage('Pre Test') {
            steps {
                sh '''
                    mvn --version
            }
        }

        stage('Test') {
            /*environment {
              TOMCAT = credentials('tomcat_user')
            }*/
        
            steps {
                //snDevOpsStep()
                sh '''
                    mvn --version
                '''
            }
            post {
                success {
                    junit '**/target/surefire-reports/*.xml' 
                }
            }
        }

        stage('Publish') {
            /*environment {
              TOMCAT = credentials('tomcat_user')
            }*/
            
            steps {
                sh 'echo publish stage'
                archiveArtifacts artifacts: 'target/**/*.war', fingerprint: true
                //snDevOpsStep()
                //snDevOpsArtifact(artifactsPayload:"""{"artifacts": [{"name": "globex-web.war","version":"2.${env.BUILD_NUMBER}.0","semanticVersion": "2.${env.BUILD_NUMBER}.0","repositoryName": "Repo1"}]}""")
                //sh 'curl -u $TOMCAT_USR:$TOMCAT_PSW --location --request PUT \'http://tomcat:8080/manager/text/deploy?path=/globex&war=globex-web.war&update=true\' --header \'Content-Type: application/java-archive\' --data-binary \'@target/globex-web.war\''
            }
        }
    }
}
