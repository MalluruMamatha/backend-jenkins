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

    environment{

        def appversion = '' // variable declaration
    }

   stages{

        stage('read version'){
            steps{
                script{
                    def packageJSON = readJSON file: 'package.json' // here we are reading the package.json file
                    appversion = packageJSON.version // in the package.json file we are getting the version
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

                /// zip -r <filename>.zip <which file you want to zip> 
                // * --> means all files will include 
                // -x Jenkinsfile-----> means we are excluding the Jenkinsfile 

        stage('build'){
            steps{
                sh """
                zip -q -r backend-${appversion}.zip * -x Jenkinsfile -x backend-${appversion}.zip
                ls -ltr
                """
            }
        }
           
    }

    post{

        always{
            echo 'always say hello' 
            //deleteDir()  ////delete workspace when build is done
        }
        success{
            echo 'i will run when pipeline is success'

        }
        failure{
            echo 'i will run when pipeline is failure'

        }
    }
}



