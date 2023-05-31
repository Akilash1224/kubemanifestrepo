pipeline {
    agent { label 'master' }
    
    stages {
        stage('Clone repository') {
            steps {
                checkout scm
            }
        }
        
        stage('Update GIT') {
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        script {
                            sh "git config user.email akilashsathyam007@gmail.com"
                            sh "git config user.name Akilash"
                            sh "cat deployment.yaml"
                            sh "sed -i 's+akilash1224/test.*+akilash1224/test:${DOCKERTAG}+g' deployment.yaml"
                            sh "cat deployment.yaml"
                            sh "git add ."
                            sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                            sh "git push https://${URLEncoder.encode(GIT_USERNAME, 'UTF-8')}:${URLEncoder.encode(GIT_PASSWORD, 'UTF-8')}@github.com/${GIT_USERNAME}/kubernetesmanifest.git HEAD:main"

                        }
                    }
                }
            }
        }
    }
}
