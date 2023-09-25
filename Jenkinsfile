node {

    def app
    stage('Clone repository') {

        checkout scm
    }

    stage('Update Git') {

        script {
            catchError(buildResult: "Success", stageResult: "FAILURE") {
                withCredentials([usernamePassword(credentialsId: 'github', passwordVariable:'GIT_PASSWORD', usernameVariable:'GIT_USERNAME')]){
                    sh "git config user.email chinedunsidinanya@yahoo.com"
                    sh "git config user.name chinedunsidinanya"
                    sh "cat deployment.yaml"
                    sh "sed -i 's+chinedunsidinanya/test.*+chinedunsidinanya/test:${DOCKERTAG}+g' deployment.yaml"
                    sh "cat deployment.yaml"
                    sh "git add ."
                    sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                    sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kubernetesmanifest HEAD:main"
                }
            }
        }
    }
}
