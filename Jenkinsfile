pipeline {
    agent none

    environment {
        AUTHOR  = "Rizky Syafrullah"
        EMAIL   = "rizkysyafrullah@gmail.com"
        WEB     = "https://www.linkedin.com/in/rizky-syafrullah-756370170/"

    }

    // triggers{
    //     cron("*/5 * * * *")
    // }

    parameters {
        string(name: 'NAME', defaultValue: 'Guest', description:'What is ur name?')
        text(name: 'DESCRIPTION', defaultValue: 'Guest', description:'tell me bout u')      
        booleanParam(name: 'DEPLOY', defaultValue: false, description:'Need to deploy?')
        choice(name: 'SOCIAL_MEDIA', choices: ['Tiktok', 'Facebook', 'Twitter'], description:'which social med?')
        password(name: "SECRET", defaultValue: '', description:'Encrypt key')
        
    }

    options {
        disableConcurrentBuilds()
        timeout(time: 3, unit: 'MINUTES')
    }
    

    stages { //didalam stages ada stage, nah di dalem stage nya dikasih multi stages

        stage('Preparation'){
            
                parallel{
                    stage("Prepare Java") {
                        agent {
                            node{
                                label "linux && java11"
                            }
                        }
                        steps {
                            echo 'Preparing Java'
                            sleep(5)
                        }
                    }
                        
                    stage("Prepare Maven") {
                        agent {
                            node{
                                label "linux && java11"
                            }
                        }                    
                        steps {
                            echo 'Preparing Maven'
                            sleep(5)
                        }
                    }       
                }         
        }

        stage("Parameter"){
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
            input {
                message "Can we Deploy??"
                ok "yess, of coursee!"
                submitter "user2,kydm"
                parameters{
                    choice(name: "TARGET_ENV", choices: ['DEV','QA','PROD' ], description: "Which Environment?")
                }
            }
            agent {
                node{
                    label "linux && java11"
                }
            }
            steps {              
                echo "Deploy to ${TARGET_ENV}"
            }
        }

        stage("Release") {

            when {
                expression {
                    return params.DEPLOY
                }
            }

            agent {
                node {
                    label "linux && java11"
                }
            }

            steps {
                echo ("Release it!")
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