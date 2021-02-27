pipeline{
    agent { label 'ubuntunode1'}
    triggers{
       cron('59 23 * * *')
      // cron('* * * *')
    }
    stages{
        stage('scm') {
            steps{
                git branch: 'qa', url:'https://github.com/mallikarjunagutta/springpetclinic-multibranch.git'
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
        post
        {
        always
           {
            mail to: 'mallikarjuna9999@outlook.com',
            subject: "Status of the pipeline ${currentBuild.fullDisplayName}",
               body: "${env.BUILD_URL} has the result as ${currentBuild.result}"
            }
        }
    }
}