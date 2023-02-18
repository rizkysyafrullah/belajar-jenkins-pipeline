pipeline {
    agent none

    environment {
        AUTHOR  = "Rizky Syafrullah"
        EMAIL   = "rizkysyafrullah@gmail.com"
        WEB     = "https://www.linkedin.com/in/rizky-syafrullah-756370170/"

    }

    parameters {
        string(name: "NAME", defaultValue: "Guest", description:"What is yor name?")
        text(name: "DESCRIPTION", defaultValue: "Guest", description:"Tell me about You")      
        booleanParam(name: "DEPLOY", defaultValue: false, description:"Need to Deploy?")
        choice(name: "SOCIAL_MEDIA", choices: ['Instagram', 'Facebook', 'Twitter', 'TikTok'], description:"Which Social Media?")
        password(name: "SECRET", defaultValue: "", description:"Encrypt Key ")
        
    }

    options {
        disableConcurrentBuilds()
        timeout(time: 3, unit: 'MINUTES')
    }

    stages("Parameter") {
        agent {
                node{
                    label "linux && java11"
                }
            }
        steps {
                echo "Hello ${params.NAME}!"
                echo "Your description is ${params.DESCRIPTION}"
                echo "Your socmed is :${params.SOCIAL_MEDIA}"
                echo "Need to deploy: ${params.DEPLOY} to deploy!"
                echo "You secret is ${params.SECRET}!"

            }
    }

    stages {

        stage('Prepare') {

            environment {
                APP = credentials("rizky_rahasia")
            }

            agent {
                node{
                    label "linux && java11"
                }
            }
            steps {
                echo("Author        : ${AUTHOR}")
                echo("email         : ${EMAIL}")
                echo("Web           : ${WEB}")
                echo("Start Job     : ${env.JOB_NAME}")
                echo("Start Build   : ${env.BUILD_NUMBER}")
                echo("Branch Name   : ${env.BRANCH_NAME}")
                echo("App User      : ${APP_USR}")
                //echo("App Password  : ${APP_PSW}")
                sh('echo "App Password : $APP_PSW" > "rahasia.txt" ')
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