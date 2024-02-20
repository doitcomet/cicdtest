pipeline {
    agent any 
    stages {
        stage('git scm update') {
            steps {
                git url: 'https://github.com/doitcomet/cicdtest.git', branch: 'main'
            }
        }
        stage('docker build and push') {
            steps {
                sh '''
                sudo docker build -t  doitcomet/cicdtest:green .
                sudo docker push doitcomet/cicdtest:green 
                '''
            }
        }
        stage('deploy and service') {
            steps {
                sh '''
                kubectl create deployment pl-bulk-prod --image=doitcomet/cicdtest:green
                kubectl expose deployment pl-bulk-prod --type=LoadBalancer --port=80 --target-port=80 --name=pl-bulk-prod
                '''
            }
        }
    }
}
