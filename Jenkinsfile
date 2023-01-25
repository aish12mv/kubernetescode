node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Build image') {
         app = docker.build("hclsw-gcp-xai/jenkins/testimg")
        //steps {
//             sh 'echo "gcloud build2"'
//                 //Build the docker image
//                 sh'''
//                     # Build the image
//                    // $(gcloud container clusters get-credentials xai-dev --zone us-east4-a --project hclsw-gcp-xai)
//                     docker build . -t hclsw-gcp-xai/jenkins
//                 '''
            //}
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
//         steps {
//             withEnv(['GCLOUD_PATH=/var/jenkins_home/google-cloud-sdk/bin']) {
//                 sh '$GCLOUD_PATH/gcloud --version'
//                 sh "$GCLOUD_PATH/gcloud builds submit --tag gcr.io/hclsw-gcp-xai/jenkins/test ."
//             }


//          } $(aws ecr get-login --region eu-west-1 --profile global --no-include-email)
        
  
      
        //sh 'echo "gcloud build2"'
       //sh "gcloud builds submit --tag gcr.io/hclsw-gcp-xai/jenkins/test ."
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
        
    
        
//         docker.withRegistry('https://gcr.io/') {
//             app.push("${env.BUILD_NUMBER}")
//             app.push("latest")
//         }
        
//         script{
//             docker.withRegistry('gcr.io/hclsw-gcp-xai/jenkins', 'ecr:us-east-2:aws-credentials') {
//             app.push("${env.BUILD_NUMBER}")
//             app.push("latest")
//             }
//         }
        
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push("${env.BUILD_NUMBER}")
        }
    }
    
    stage('Trigger ManifestUpdate') {
                echo "triggering updatemanifestjob"
                build job: 'updatemanifest', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
        }
}
