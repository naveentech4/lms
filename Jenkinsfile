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
                sh 'cd webapp && npm install && npm run build'                
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
                    sh 'sudo rm -rf /var/www/html/*'
                    sh 'sudo cp -r webapp/dist/* /var/www/html'                    
            }
            }
        }

    }
}
