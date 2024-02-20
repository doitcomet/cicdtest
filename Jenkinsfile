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
                sudo docker build -t doitcomet/cicdtest:green .
                sudo docker push doitcomet/cicdtest:green
                '''
            }
        }
        stage('deploy and service') {
            steps {
                sh '''
                ansible master -m command -a 'kubectl create deploy web-green --replicas=3 --image=doitcomet/cicdtest:green'
                ansible master -m command -a 'kubectl expose deploy web-green --type=LoadBalancer --port=80 --target-port=80 --name=web-green-svc'
                '''
            }
        }
    }
}
