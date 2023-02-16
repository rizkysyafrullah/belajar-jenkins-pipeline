pipeline {
    agent {
        node{
            label "linux && java11"
        }
    }
    
    stages {
        
        stage('Build') {
            steps {
                echo 'Hello Build'
            }
        }

        stage('Test') {
            steps {
                echo 'Hello Test'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Hello Deploy'
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