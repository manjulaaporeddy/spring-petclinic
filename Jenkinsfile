pipeline {
    agent { label 'BUILD'}
    triggers {
        cron('H * * * *')
        pollSCM('* * * * *')
    }
    parameters {
        string(name: 'BRANCH', defaultValue: 'main', description: 'Branch to build' )
    }
    environment {
        CI_ENV = 'DEV'
    }
    stages {
        stage('scm') {
            environment {
                DUMMY = 'FUN'
            }
            steps {
                
                git branch: "${params.BRANCH}", url: 'https://github.com/manjulaaporeddy/spring-petclinic.git'
                //input message: 'Continue to next stage? ', submitter: 'qtaws,qtazure'
                echo env.CI_ENV
                echo env.DUMMY
            }
        }
        stage('build') {
            steps {
                echo env.GIT_URL
                sh 'mvn package'
            }
        }
    }
    post {
        success {
            archive '**/gameoflife.war'
            junit '**/TEST-*.xml'
        }
        
    }
}