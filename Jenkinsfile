node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                      
                        sh "git config user.email akshayanarayanamgmail.com"
                        sh "git config user.name AkShaYa165432"
                      
                        sh "cat deployment.yaml"
                        sh "sed -i 's+akshaya23/packages.*+akshaya23/packages:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'By Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/K8s-Manifests.git HEAD:main" 
      }
    }
  }
}
}
