node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email danirg2222@outlook.es"
                        sh "git config user.name DanielRamirez1901"
                        //sh "git switch master"
                        sh "cat knote.yaml"
                        sh "sed -i 's+ventana1901/knote.*+ventana1901/knote:${DOCKERTAG}+g' knote.yaml"
                        sh "cat knote.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/CD-Jenkins-Kubernetes.git HEAD:main"
      }
    }
  }
}
}