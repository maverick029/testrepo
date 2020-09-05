pipeline{
    agent any
    stages{
        stage('build'){
            agent {

                dockerfile {
                    filename 'Dockerfile'
                    dir 'build'
                    args '-v $PWD:/home/codefiles'
                            }
                }
            steps{
                sh label: '', script: 'cd /home/codefiles'

                git changelog: false, credentialsId: '<git_credential>', poll: false, url: '<git url for app>'
                sh label: '', script: 'ls -a'
                sh label: '', script: 'mvn package'
            }
            post {
                success {
                        archiveArtifacts artifacts: 'target/*.war', fingerprint: true
                        }
                    failure {
                        mail to: '<recipient>', subject: "Build Failed: ${currentBuild.fullDisplayName}",body: "This is the build ${env.BUILD_URL}"
                        cleanWs()
                        }
                }

        }
    }
}

