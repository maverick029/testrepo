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
        }
    }

}
