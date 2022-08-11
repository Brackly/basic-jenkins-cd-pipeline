def gv

pipeline{
    tools{
        maven 'Maven'
    }
    parameters{
        choice(name: 'VERSION', choices:['1.2','1.3','1.4'], description:'')
        booleanParam(name: 'executeTests', defaultValue:true, description:'')
    }
    agent any
    environment{
        NEW_VERSION='1.3.2'
        SERVER_CREDENTIALS=credentials('')
    }
    stages{
        stage('init'){
            script{
                gv = load "script.groovy"
            }
        }

        stage('build'){
            script{
                gv.buildApp()
            }
        }

        stage('test'){
            when{
                expression{
                    params.executeTests==true //will only execute if executeTestes is not false
                }
            }
            script{
                gv.testApp()
            }
        }
        stage('deploy'){
            script{
                gv.deployApp()
            }
        }
        // post{
        //     always{

        //     }
        //     success{

        //     }
        //     failure{

        //     }
        // }
    }
}