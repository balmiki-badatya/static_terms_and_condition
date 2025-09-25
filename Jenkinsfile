pipeline {
    agent any

    environment{
        STATIC_TERMS_PAGE_CLOUDFRONT_DISTRIBUTION_ID = credentials('STATIC_TERMS_PAGE_CLOUDFRONT_DISTRIBUTION_ID')
    }

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
        stage("Invalidate CloudFront Cache") {
            steps {
                sh '''
                    aws cloudfront create-invalidation \
                        --distribution-id ${STATIC_TERMS_PAGE_CLOUDFRONT_DISTRIBUTION_ID} \
                        --paths "/*"
                    '''
            }
        }
    }

}