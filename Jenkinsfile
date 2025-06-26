pipeline {
    agent any
    triggers {
        pollSCM '* * * * *'
    }
    stages {
        stage('Build') {
            steps {
                echo "Building.."
                sh '''
                cd app
                pip3 install --user -r requirements.txt
                '''
            }
        }
        stage('Test') {
            steps {
                echo "Testing.."
                sh '''
                cd app
                python3 hello.py
                python3 hello.py --name=Niteesh
                '''
            }
        }
        stage('Deliver') {
            steps {
                echo 'Deliver....'
                sh '''
                mkdir -p app/output
                echo "Delivery successful for Niteesh!" > app/output/deliver.txt
                '''
            }
        }

        stage('Archive') {
            steps {
                echo 'Archiving delivery file...'
                archiveArtifacts artifacts: 'app/output/deliver.txt', allowEmptyArchive: false
            }
        }
    }
}
