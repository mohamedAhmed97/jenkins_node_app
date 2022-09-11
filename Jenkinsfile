pipeline{
    agent any

    stages{
        stage("preparation"){
            steps{
                echo "========stage preparation ========"
                git "https://github.com/mohamedAhmed97/jenkins_node_app.git"
            }
        }

         stage("building"){
            steps{
                echo "========stage building ========"
                sh "docker build -t mar97/node_app:1.1 ."
            }
        }

        stage("deployment"){
            steps{
                echo "========stage deployment ========"
               withCredentials([usernamePassword(credentialsId: 'docker-hub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh "echo $PASSWORD | docker login -u $USERNAME --password-stdin"
                    sh "docker push mar97/node_app:1.1" 
                }
            }
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
            slackSend(color:#0fff,message:"hi")
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}