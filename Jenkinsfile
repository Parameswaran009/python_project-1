node {
    def app

    stage('Build image') {
  
       app = docker.build("parameswaran/argocd")
    }

    stage('Push image') {
        
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push("${env.BUILD_NUMBER}")
        }
    }
    
    stage('Trigger ManifestUpdate') {
                echo "triggering updatemanifestjob"
                build job: 'Python-job2', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
        }
}
