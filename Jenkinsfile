node {
    def app
    stage('Clone repository') {
        checkout scm
    }
    stage('Update GIT') {
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                    sh "git config user.email techednelson@gmail.com"
                    sh "git config user.name Nelson Sandoval"
                    sh "cat deployment.yml"
                    sh "sed -i 's+webtechnelson/ci-test-image.*+webtechnelson/ci-test-image:${DOCKERTAG}+g' deployment.yml"
                    sh "cat deployment.yml"
                    sh "git add ."
                    sh "git commit -m 'Done by Jenkins Job updatek8PipelineGitOps: ${env.BUILD_NUMBER}'"
                    sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/k8-pipeline-GitOps.git HEAD:main"
                }
            }
        }
    }
}