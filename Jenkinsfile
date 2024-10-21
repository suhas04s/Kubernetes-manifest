node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Update GIT') {
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                    sh "git config user.name 'suhas1996s'"
                    sh "cat i18next-app_deployment.yaml"
                    sh "sed -i 's+suhas1996s/i18next-app.*+suhas1996s/i18next-app:${DOCKERTAG}+g' i18next-app_deployment.yaml"
                    sh "cat i18next-app_deployment.yaml"
                    sh "git add ."
                    sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                    sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/Kubernetes-manifest.git HEAD:main"
                }
            }
        }
    }
}
