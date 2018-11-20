pipeline {
    agent any

    environment {
        ORIGIN_ACCENTURE = 'https://gitlab.sdc.accenture.com/iberdrola/svn-git-piloto.git'
        ORIGIN_IBERDROLA = 'github.com/oscuroweb/spring-petclinic.git'
        
    }

    triggers {
        pollSCM 'H/5 * * * *'
    }

    stages {
        
        stage('Compile') {
            steps {
                sh "Compiling"
            }
        }
        
        stage('Unit Tests') {
            steps {
                sh "Testing"
            }
        }
        
        stage('Code Quality Tests') {
            steps {
                sh "Quality test running"
            }
        }

        stage('Copy to Iberdrola repository') {
            environment {
                CREDENTIALS_IBERDROLA = credentials('GitHub')
            }

            steps {
                sh "Copying to Iberdrola repository"
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