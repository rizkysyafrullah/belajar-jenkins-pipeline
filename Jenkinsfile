pipeline {
    agent none

    stages {

        stage('Prepare') {
            agent {
                node{
                    label "linux && java11"
                }
            }
            steps {
                echo("Start Job     : ${env.JOB_NAME}")
                echo("Start Build   : ${env.BUILD_NUMBER}")
                echo("Branch Name   : ${env.BRANCH_NAME}")
            }
        }
        
        stage('Build') {
            agent {
                node{
                    label "linux && java11"
                }
            }
            steps {

                script{
                    for (int i = 0; i < 10 ; i++) {
                        echo("Script ${i}")
                    }
                }

                echo 'Start Build'
                sh'./mvnw clean compile test-compile'
                echo 'Finish Build'
            }
        }

        stage('Test') {
            agent {
                node{
                    label "linux && java11"
                }
            }
            steps {

                script {
                    def data = [
                        "firstName" : "Rizky",
                        "lastName"  : "Syafrullah"
                    ]
                    writeJSON(file: "data.json", json: data)
                }

                echo 'Start Test'
                sh'./mvnw test'
                echo 'Finish Test'
            }
        }

        stage('Deploy') {
            agent {
                node{
                    label "linux && java11"
                }
            }
            steps {              
                echo 'Hello Deploy 1'
                sleep(5)
                echo 'Hello Deploy 2'
                echo 'Hello Deploy 3'
            }
        }

    }

    post{
        always{
            echo 'i will always say Hello Again !!'
        }
        success{
            echo 'Yeahh, its success!'
        }
        failure{
            echo 'Oh Noo, its faill :( '
        }
        cleanup{
            echo    'dont care success or not :) '
        }
    }
}