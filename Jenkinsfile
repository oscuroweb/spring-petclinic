pipeline {
    agent any

    environment {
        DISABLE_AUTH = 'true'
        DB_ENGINE    = 'sqlite'
        ORIGIN_ACCENTURE = 'https://gitlab.sdc.accenture.com/iberdrola/svn-git-piloto.git'
        ORIGIN_IBERDROLA = 'https://github.com/oscuroweb/spring-petclinic.git'
        
    }

    stages {
        
        stage('Compile') {
            steps {
                sh "echo ${env.GIT_LOCAL_BRANCH}"
                sh "echo ${env.ORIGIN_ACCENTURE}"
                sh "echo ${env.ORIGIN_IBERDROLA}"
            }
        }
        
        stage('Unit Tests') {
            steps {
                sh "echo ${env.GIT_LOCAL_BRANCH}"
            }
        }
        
        stage('Code Quality Tests') {
            steps {
                sh "echo ${env.GIT_LOCAL_BRANCH}"
            }
        }

        stage('Copy to Iberdrola repository') {
            environment {
                CREDENTIALS_IBERDROLA = credentials('GitHub')
            }
            steps {
                sh "echo ${env.GIT_LOCAL_BRANCH}"
                sh "git checkout ${env.GIT_LOCAL_BRANCH}"
                sh "git remote remove origin"
                sh "git remote add origin ${env.ORIGIN_IBERDROLA}"

                sh "git push origin ${env.GIT_LOCAL_BRANCH}"
            }
        }
    }
}