node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'gitlablocal', passwordVariable: 'GIT_TOKEN', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email syachferdian4@gmail.com"
                        sh "git config user.name ekazfarm"
                        //sh "git switch master"
                        sh "cat /deploy/default/deployment.yaml"
                        sh "sed -i 's+ekawafs/htmlcicd.*+ekawafs/htmlcicd:${DOCKERTAG}+g' /deploy/default/deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push http://${GIT_USERNAME}:${GIT_TOKEN}@gitlab.example.com/${GIT_USERNAME}/htmlcicd-kubemanifest.git HEAD:main"
      }
    }
  }
}
}
