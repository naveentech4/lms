pipeline {
    agent any
    
    stages {
        stage('Sonar Analysis') {
            steps {
                echo 'test hook..'
                sh 'cd webapp && sudo docker run  --rm -e SONAR_HOST_URL="http://34.16.145.218:9000" -e SONAR_LOGIN="sqp_d06d93c12f94870c7843b727df7b02eabb05fe51"  -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms'      
            }
        }


        stage('Build LMS') {
            steps {
                script{
                    echo 'Building..'
                    def packageJson=readJSON file:'webapp/package.json'
                    def packageJSONVersion=packageJson.version
                    sh "echo '${packageJSONVersion}'"
                    sh 'cd webapp && npm install && npm run build'                
                }                
            }
        }

        stage('Release LMS') {
            steps {
                script {
                    echo "Releasing.."  
                    def packageJson=readJSON file:'webapp/package.json'
                    def packageJSONVersion=packageJson.version  
                    sh "cd webapp && zip dist-${packageJSONVersion}.zip -r dist"
                    sh "curl -u admin:nk@123 -X GET \'http://34.16.145.218:8081/repository/lms/dist-${packageJSONVersion}.zip\' --output dist-'${packageJSONVersion}'.zip"
                    sh 'ls webapp'                       
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
