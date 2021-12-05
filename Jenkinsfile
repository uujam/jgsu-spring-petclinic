pipeline {
    agent any
    triggers { pollSCM('* * * * *')}
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/uujam/jgsu-spring-petclinic.git'
            }
        }
        stage('Build') {
            steps {
                //sh './mvnw clean package'
                sh 'true'
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                always {
                    //junit '**/target/surefire-reports/TEST-*.xml'
                    //archiveArtifacts 'target/*.jar'
                //}
                //changed {
                    emailext attachLog: true, 
                    body: 'Please go to ${BUILD_URL} and verify the build', 
                    compressLog: true,
                    to: "me@jenkins",
                    recipientProviders: [upstreamDevelopers(), requestor()], 
                    subject: 'Job \'${JOB_NAME}\' (${BUILD_NUMBER}) is waiting for input'
                }
            }
        }
    }
}
