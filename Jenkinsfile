pipeline {
    agent any

    stages {
        stage ('Compile Feature Stage') {

            steps {
                withMaven(maven : 'maven_3_5_0') {
                    bat 'mvn clean compile'
                }
            }
        }

        stage ('Testing Feature Stage') {

            steps {
                withMaven(maven : 'maven_3_5_0') {
                    sh 'mvn test'
                }
            }
        }

         stage ('Run Sonar Analysis Stage on Feature') {

            steps {
                withMaven(maven : 'maven_3_5_0') {
                    sh """mvn sonar:sonar \
                         -Dsonar.projectKey=abc_sonar \
                         -Dsonar.host.url=http://34.68.137.4:9000 \
                         -Dsonar.login=7aa0f5eec8f0ef469314e6b95f4c18ce822b0891"""
                }
            }
        }               
                
         stage ('Deploy To Nexus Feature Stage') {

            steps {
                withMaven(maven : 'maven_3_5_0') {
                    sh 'mvn deploy'
                }
            }
        }       
        
    }
}
