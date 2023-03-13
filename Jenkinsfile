
node {
    def app

    stage('Clone repository') {
        //sh 'pip install pylint'
        checkout scm
    }

    stage('Build image') {
        // app = docker.build("testimg")
        app = docker.build("aishwaryamv/test")
    }
    
    stage('Test image') {
       // app.inside {
           // sh 'echo "Tests passed"'
       // }
    }

    stage('Push image') {

//       sh "docker tag testimg gcr.io/hclsw-gcp-xai/jenkins/testimg:latest"
//         sh "docker push gcr.io/hclsw-gcp-xai/jenkins/testimg:latest"
//         docker.withRegistry('https://gcr.io/hclsw-gcp-xai', 'newauth') {
//             sh "docker tag testimg gcr.io/hclsw-gcp-xai/jenkins/testimg:latest"
//             app.push("${env.BUILD_NUMBER}")
//             app.push("latest")
//         }
//         docker.withRegistry('gcr.io/hclsw-gcp-xai/jenkins') {
//             app.push("${env.BUILD_NUMBER}")
//             app.push("latest")
//             }
        

        
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push("${env.BUILD_NUMBER}")
        }
    }
    
    stage('Trigger ManifestUpdate') {
                echo "triggering updatemanifestjob"
                build job: 'updatemanifest', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
        }
}
