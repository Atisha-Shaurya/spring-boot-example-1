pipeline{
    agent any
    tools { 
        maven 'maven3'
    }
    stages
       {
            stage("clean")
            {
                steps{
                    sh "mvn clean"
                }
            }
            stage("Build")
            {
                steps{
                    sh "mvn compile"
                }
                
            }
            stage("TEST")
            {
                steps{
                    sh "mvn test"
                }
            }
            stage("package")
            {
                steps{
                    sh "mvn package"
                }
            }
    stage("Deploy")
            {
                steps{
                    sshagent(['Atishashauryaa']) {
                    sh "scp -o StrictHostKeyChecking=no  /home/.jenkins/workspace/Final_project_prod/target/*.jar 3.89.20.209@172.31.91.96:/home/ubuntu/"
                               
                 }
                }
            }    
    }
    post {
        always{
            mail to: 'atisha.shaurya@knoldus.com',
			subject: "Pipeline: ${currentBuild.fullDisplayName} is ${currentBuild.currentResult}",
			body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}"
        }

     }
}
sshagent(['Atishashauryaa']) {
    // some block
}
