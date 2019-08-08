@Library('my-shared-library') _

//evenOrOdd(currentBuild.getNumber())
//log.info 'Starting'
//log.warning 'Nothing to do!'

pipeline {
    agent any
    
    stages {
        stage('Git Checkout') {
            steps {
            gitCheckout(
                branch: "Feature",
                url: "https://github.com/MyInfosys/ABC.git"
                )
            }
        }
        
        stage ('Clean Compile Test Package Feature Stages') {

            steps {
                withMaven(maven : 'maven_3_5_0') {
                    script {
                         maven.mavenGoals()
                    }
                }
            }
        }     
         stage ('Run Sonar Analysis Stage on Feature') {

            steps {
                withMaven(maven : 'maven_3_5_0') {
                    script {
                         sonar.sonarScan()
                    }
                }
            }
        }               
                
         stage ('Deploy To Nexus Feature Stage') {

            steps {
                withMaven(maven : 'maven_3_5_0') {
                    script {
                         nexus.nexusDeploy()
                    }
                }
            }
        }                
    }
}
