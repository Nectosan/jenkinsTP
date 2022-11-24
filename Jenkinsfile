pipeline{

    agent any

    tools{
            maven 'maven'
            jdk 'jdk-11.0.16.1'
        }

        stages{
            stage('git checkout'){
                steps{
                    git credentialsId:'credentialsgit',url:'https://github.com/Nectosan/jenkinsTP'
                }
            }

            stage('Build the application'){
                steps{
                    bat 'mvn clean install'
                }
            }

            stage('Unit Test Execution'){
                steps{
                    bat 'mvn test'
                }
            }
            stage('Build the docker image') {
                steps{
                    withCredentials([usernameColonPassword(credentialsId: 'dockerhubpass', variable:'dockerHubPass')]){

                        bat """docker login -u rihci -p Dubacu60!=RC"""
                    }
                    bat "docker build -t rihci/triang7:1.0.0 ."
                    bat "docker push rihci/triang7:1.0.0"
                }
            }

        }


}



