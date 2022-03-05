pipeline {
    agent any ;

    tools {
        maven 'maven3.8.4'
    }
    triggers{ //(use anyone basedon your use)
        // poll scm
        pollSCM('* * * * *')
        // Build Periodically
        //cron('* * * * *')
        // github webhook
        //githubPush()
    }
    stages {
        stage ("CheckOutCode"){
            steps{
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/divyeshbhalekar/New-project-hello.git'

            }
        }
        stage ("build"){
            steps{
                sh "mvn clean package"
            }
        }
       stage ("appln-deployed"){
            steps{ 
                sshagent(['55a8a4eb-bb93-4618-a4fb-c91fffeeccc9']) {
            sh "scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/demo/webapp/target/webapp.war ec2-user@3.86.160.237:/home/ec2-user/apache-tomcat-9.0.59/webapps/"
            }

            }
        }

    }
}
