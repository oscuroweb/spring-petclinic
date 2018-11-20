pipeline {
    agent any

    environment {
        DISABLE_AUTH = 'true'
        DB_ENGINE    = 'sqlite'
        ORIGIN_ACCENTURE = 'https://gitlab.sdc.accenture.com/iberdrola/svn-git-piloto.git'
        ORIGIN_IBERDROLA = 'github.com/oscuroweb/spring-petclinic.git'
        
    }

    triggers {
        pollSCM 'H/5 * * * *'
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
                withCredentials([usernamePassword(credentialsId: 'GitHub', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                    sh "git remote add origin https://${GIT_USERNAME}:'${GIT_PASSWORD}'@${env.ORIGIN_IBERDROLA}"
                    sh "git push origin ${env.GIT_LOCAL_BRANCH}"
                }
            }
        }
    }
}