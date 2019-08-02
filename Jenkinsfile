pipeline {
    agent any

    stages {
        stage ('Compile Feature Stage') {

            steps {
                withMaven(maven : 'maven_3_5_0') {
                    sh 'mvn clean compile'
                }
            }
        }

        stage ('Testing Feature Stage') {

            steps {
                withMaven(maven : 'maven_3_5_0') {
                    sh 'mvn test'
                    sh "echo ${env.CHANGE_ID}"
                }
            }
        }

         stage ('Run Sonar Analysis Stage on Feature') {
            steps {
                //def PULL_REQUEST = ${env.CHANGE_ID}
                withMaven(maven : 'maven_3_5_0') {
                    sh 'echo "Printing pullID"'
                    sh "PULL_REQUEST= ${env.CHANGE_ID}"
                    sh 'echo $PULL_REQUEST'
                    sh """mvn sonar:sonar \
                         -Dsonar.projectKey=abc_sonar \
                         -Dsonar.host.url=http://34.68.137.4:9000 \
                         -Dsonar.login=7aa0f5eec8f0ef469314e6b95f4c18ce822b0891
                         -Dsonar.github.pullRequest=${PULL_REQUEST} \
                         -Dsonar.github.oauth=c55a2490b57a3f3f4bc28367cf784c25683b0c04"""
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
