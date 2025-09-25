pipeline {
    agent any

    stages {

        stage("Clean Workspace") {
            steps {
                cleanWs()
            }
        }
        stage("Git Clone") {
            steps {
                git branch: 'master',
                    url: 'https://github.com/balmiki-badatya/static_terms_and_condition.git'
            }
        }
        stage("Push to s3") {
            steps {
                sh 'aws s3 cp index.html s3://static-terms-condition --region us-west-1'
            }
        }
    }

}