pipeline {
    agent any

    stages {
        stage('Sonar Analysis') {
            steps {
                echo 'Testing..'
                
            }
        }

        stage('Build LMS') {
            steps {
                echo 'Building..'
                
            }
        }

        stage('Release LMS') {
            steps {
                script {
                    echo "Releasing.."       
                    
            }
            }
        }

        stage('Deploy LMS') {
            steps {
                script {
                    echo "Deploying.."       
            }
            }
        }


    }
}
