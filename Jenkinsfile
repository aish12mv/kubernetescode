node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Build image') {
//         steps {
                
//                 git branch: 'patch-1', url: 'gitrepository'

//                 sh "mvn clean package"
                
//                 script {
//                      dockerImage = docker.build registry
//                       }
//                 script {
//                            docker.withRegistry( '', registryCredential ) {
//                                 dockerImage.push()
//                            }
//                 }    

               
//             }
  
       app = docker.build("hclsw-gcp-xai/jenkins")
    }

    stage('Test image') {

       // app.inside {
           // sh 'echo "Tests passed"'
       // }
    }

    stage('Push image') {
//         withCredentials([file(credentialsId: 'gcr', variable: 'GC_KEY')]){
//               sh "cat '$GC_KEY' | docker login -u _json_key --password-stdin https://eu.gcr.io"
//               sh "gcloud auth activate-service-account --key-file='$GC_KEY'"
//               sh "gcloud auth configure-docker"
//               GLOUD_AUTH = sh (
//                     script: 'gcloud auth print-access-token',
//                     returnStdout: true
//                 ).trim()
//               echo "Pushing image To GCR"
//               sh "docker push eu.gcr.io/${google_projectname}/${image_name}:${image-tag}"
//           }
        
    
        
        docker.withRegistry('https://us.gcr.io') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
        
//         script{
//             docker.withRegistry('gcr.io/hclsw-gcp-xai/jenkins', 'ecr:us-east-2:aws-credentials') {
//             app.push("${env.BUILD_NUMBER}")
//             app.push("latest")
//             }
//         }
        
//         docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
//             app.push("${env.BUILD_NUMBER}")
//         }
    }
    
    stage('Trigger ManifestUpdate') {
                echo "triggering updatemanifestjob"
                build job: 'updatemanifest', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
        }
}
