pipeline{
    agent {
        label 'agent-1'
    }
    options{ /// using option we can specify the time that pipeline should execute 
    //(with in the time it get complets)
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
        ansiColor('xterm')
       
    }

   stages{

        stage('read version'){
            steps{
                script{
                    def packageJSON = readJSON file: 'package.json'
                    def appversion = packageJSON.version
                    echo "application version is: $appversion"
                }
            }
        }

        stage('install dependencies'){
            steps{
                sh """
                 npm install
                 ls -lt
                 echo "application version is: $appversion"
                """
           
            }
        }
           
    }

    post{

        always{
            echo 'always say hello' 
            deleteDir()  ////delete workspace when build is done
        }
        success{
            echo 'i will run when pipeline is success'

        }
        failure{
            echo 'i will run when pipeline is failure'

        }
    }
}



