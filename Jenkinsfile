pipeline {
    agent any
    stages{
        stage("Git Checkout"){
            steps{
               git branch: 'main', credentialsId: 'deploy', url: 'https://github.com/Sahana7798/node-repo1.git'
            }
        }
        stage("Build and Test"){
            steps{
                sh "docker build -t sahanalohith/newimage1 ."
            }
        }
        stage("login and push"){
            steps{
                withCredentials([string(credentialsId: 'devops', variable: 'devops')]) {
                    sh "docker login -u sahanalohith -p ${devops}"
                }
                sh "docker push sahanalohith/newimage1"
            }
        }
        stage ("Deploy"){
            steps{
                sshagent(['new']) {
}
              sh "ssh -o StrictHostkeyChecking=no ec2-user@3.83.237.130 docker run -d -p 6000:8000 --name qwerty sahanalohith/newimage1"
            }
        }
    }
}
           
    
