node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Update GIT') {
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                    sh "git config user.email danirg2222@outlook.es"
                    sh "git config user.name DanielRamirez1901"
                    
                    // Path to the values.yaml in the Helm chart directory
                    def valuesYamlPath = 'helm-project/values.yaml'
                    
                    // Update the image tag in the values.yaml file
                    sh "sed -i 's+tag:.*+tag: ${DOCKERTAG}+g' ${valuesYamlPath}"
                    
                    // Display the updated file for verification
                    sh "cat ${valuesYamlPath}"
                    
                    // Commit and push the changes to the repository
                    sh "git add ${valuesYamlPath}"
                    sh "git commit -m 'Update image tag to ${DOCKERTAG} by Jenkins Job: ${env.BUILD_NUMBER}'"
                    sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/CD-Jenkins-Kubernetes.git HEAD:main"
                }
            }
        }
    }
}
