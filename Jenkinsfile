pipeline{
    agent {
        label 'AGENT-1'
    }
    options{ /// using option we can specify the time that pipeline should execute 
    //(with in the time it get complets)
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
        ansiColor('xterm')
       
    }

   

   

    stages{
        stage('test'){
            steps{
                sh """
                    ls -ltr
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



