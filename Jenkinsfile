node ('boxcube') {
    stage('Clone') {
    echo "1.Git Clone"
   // git url: "https://github.com/Box-Cube/nginx-helloworld.git"
    script {
        build_tag = sh(returnStdout: true, script: 'echo v1').trim()
    }
    }
    stage('Build') {
    echo "2.Build Docker Image Stage"
    sh "docker build -t harbor.box.com/cicd/nginx-helloworld:${build_tag} ."
    }
    stage('Push') {
    echo "3.Push Docker Image Stage"
    sh "docker login harbor.box.com -u cicd -p Test@123"
    sh "docker push harbor.box.com/cicd/nginx-helloworld:${build_tag} "
    }
    stage('YAML') {
    echo "4. Change YAML File Stage"
    sh "sed -i 's/<BUILD_TAG>/${build_tag}/' nginx-deploy.yaml"
    }
    stage('Deploy') {
    echo "5. Deploy Stage"
    sh "kubectl apply -f nginx-deploy.yaml"
    }
}
