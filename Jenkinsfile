pipeline{
    agent { label 'ubuntunode2'}
    triggers{
        cron('H * * * 1-5')
    }
    parameters {
        string(name: 'MAVENGOAL', defaultValue: 'clean package', description: 'This is a maven goal')

        string(name: 'URL', defaultValue: 'https://github.com/mallikarjunagutta/springpetclinic-multibranch.git', description: 'url of the git')
    }
    options{
        //If time exceeds more than 3 seconds pipeline gets Aborted
            timeout(time: 3, unit: 'HOURS')
         }
    stages{
        stage('scm') {
            steps{
                git branch: 'developer', url: "${params.URL}"
                }
        }
        stage('build') {
            steps {
                sh script: "mvn ${params.MAVENGOAL}"
                //sh script: 'mvn clean package'
            }
        }
        stage('post build'){
            steps{
             junit 'target/surefire-reports/*.xml'
             archiveArtifacts 'target/*.jar'
             sh "echo developer build is successfully created!"
             stash name: 'warfile', includes: 'target/*.jar'
            }
        }
        stage('copy the build to another node after packging'){
            agent{ label 'ubuntunode1'}
            steps{
                unstash name: 'warfile'
            }
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