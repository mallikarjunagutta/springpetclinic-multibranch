pipeline{
    agent { label 'ubuntunode2'}
    stages{
        stage('scm') {
            steps{
                git branch: 'main', url:'https://github.com/spring-projects/spring-petclinic.git'
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