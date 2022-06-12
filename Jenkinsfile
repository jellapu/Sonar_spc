pipeline {
    agent { label 'build_java_11' }
    triggers { 
        cron('45 23 * * 1-5')
        pollSCM('*/5 * * * *')
    }
        
        
    stages {
        stage('scm') {
            steps {

                git url: 'https://github.com/jellapu/Sonar_spc.git', branch: 'main'
            }
        }
        stage('build') {
            steps {
                withSonarQubeEnv(installationName: 'SONAR_9.4', envOnly: true, credentialsId: 'SONAR_TOKEN') {
                    sh "/usr/local/apache-maven-3.8.5/bin/mvn clean package sonar:sonar"
					echo "${env.SONAR_HOST_URL}"

                }

            }
        }
    }

}