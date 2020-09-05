pipeline{
    agent any
    stages{
        stage('build'){
            agent {

                dockerfile {
                    filename 'Dockerfile'
                    dir 'webapp'
                    args '-v $PWD:/home/codefiles'
                            }
                }
            steps{
                sh label: '', script: 'cd /home/codefiles'

                git changelog: false, credentialsId: '<git_credential>', poll: false, url: '<git url for app>'
                sh label: '', script: 'ls -a'
                //sh label: '', script: 'mvn package'
            }
            post {
                success {
                        //archiveArtifacts artifacts: 'target/*.war', fingerprint: true
                    mail to: 'maheshpatjoshi90@gmail.com', subject: "Build Failed: ${currentBuild.fullDisplayName}",body: "This is the build ${env.BUILD_URL}"
                        }
                    failure {
                        mail to: 'maheshpatjoshi90@gmail.com', subject: "Build Failed: ${currentBuild.fullDisplayName}",body: "This is the build ${env.BUILD_URL}"
                        cleanWs()
                        }
                }

        }
    }
}

