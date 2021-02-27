pipeline{
    agent { label 'MASTER'}
    stages{
        stage('scm') {
            steps{
                git branch: 'release', url:'https://github.com/mallikarjunagutta/springpetclinic-multibranch.git'
            }
        }
        stage('build') {
            steps {
                sh script: 'mvn clean package'
            }
        }
        stage('post build'){
            steps{
             junit 'target/surefire-reports/*.xml'
             archiveArtifacts 'target/*.jar'
             sh "echo it should work now!"
          
            
            }
        }
         post{
        always{
            mail to: 'mallikarjuna9999@outlook.com',
            subject: "Status of the pipeline ${currentBuild.fullDisplayName}",
               body: "${env.BUILD_URL} has the result as ${currentBuild.result}"
        }
    }
    }
}