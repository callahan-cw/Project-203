pipeline {
    agent { label "master" }
    environment {
        PATH=sh(script:"echo $PATH:/usr/local/bin", returnStdout:true).trim()
        AWS_REGION = "us-east-1"
        AWS_ACCOUNT_ID=sh(script:'export PATH="$PATH:/usr/local/bin" && aws sts get-caller-identity --query Account --output text', returnStdout:true).trim()
        ECR_REGISTRY="${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com"
        APP_REPO_NAME = "clarusway-repo/phonebook-app"
        APP_NAME = "phonebook"
        AWS_STACK_NAME = "Call-Phonebook-App-${BUILD_NUMBER}"
        CFN_TEMPLATE="phonebook-docker-swarm-cfn-template.yml"
        CFN_KEYPAIR="call.training"
        HOME_FOLDER = "/home/ec2-user"
        GIT_FOLDER = sh(script:'echo ${GIT_URL} | sed "s/.*\\///;s/.git$//"', returnStdout:true).trim()
    }
    stages {
        stage ('Create ECR Repo'){
            steps{
                echo 'Creating ECR Repo for App'
                sh """
                aws ecr create-repository \
                  --repository-name ${APP_REPO_NAME} \
                  --image-scanning-configuration scanOnPush=false \
                  --image-tag-mutability MUTABLE \
                  --region ${AWS_REGION}
                """
            }
            
        }
        stage ('Build App Docker Image'){
            steps{
                echo 'Building App Image'

            }

        }
        stage ('Push the Image the ECR Repo'){
            steps{
                echo 'Pushing App Image to ECR Repo'

            }

        }
        stage ('Create Infrastructure for the App'){
            steps{
                echo 'Creating Infrastructure for the App on AWS Cloud'

            }

        }
        stage ('Test the Intrastructure'){
            steps{
                echo "Testing if the Docker Swarm is ready or not, by checking Viz App on Grand Master with Public Ip Address: {MASTER_INSTANCE_PUBLIC_IP}:8080"

            }

        }
        stage ('Deploy the App on Docker Swarm'){
            steps{
                echo "Cloning and Deploying App on Swarm using Grand Master with Instance Id: MASTER_INSTANCE_ID"

            }

        }
    }
    post{
        always {
            echo 'Deleting all local docker images'
        }
        failure {
            echo 'Delete the Image Repository on ECR due to the failure'
            echo 'Delete the Cloudformatino Stack due to the failure'
        }
    }

}