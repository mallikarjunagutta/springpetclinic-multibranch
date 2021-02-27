pipeline{
    agent { label 'MASTER'}
    stages{
        stage('scm') {
            steps{
                git branch: 'main', url:'https://github.com/mallikarjunagutta/springpetclinic-multibranch.git'
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
    }
}