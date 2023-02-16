pipeline {
    agent {
        node{
            label "linux && java11"
        }
    }
    
    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
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