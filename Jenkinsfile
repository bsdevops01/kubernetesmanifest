node {

    stage('Clone repository') {
        checkout scm
    }

    stage('Update Manifest') {
        withCredentials([usernamePassword(
            credentialsId: 'git-pat',
            usernameVariable: 'GIT_USERNAME',
            passwordVariable: 'GIT_PASSWORD'
        )]) {

            sh '''
            git config user.email "bshrivastava01@gmail.com"
            git config user.name "basant"

            echo "Updating deployment.yaml with new tag..."

            sed -i "s#bsdocker10/k8sdemo:.*#bsdocker10/k8sdemo:${DOCKERTAG}#g" deployment.yaml

            git add deployment.yaml
            git commit -m "Update image tag to ${DOCKERTAG}" || echo "No changes to commit"

            git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kubernetesmanifest.git main
            '''
        }
    }
}
