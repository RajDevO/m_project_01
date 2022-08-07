node {
    def app    
      
    stage('Clone repository') {      
        checkout scm
    }
    stage('Build image') {
  
       app = docker.build("kuberaj/project_001")
    }
    stage('Test image') {
            app.inside {
            sh 'echo "Tests passed"'
        }
    }
    stage('Push image') {      
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhubpwd')
         {
            
             app.push("${env.BUILD_NUMBER}")
            
         }
    }
            
   stage('Manifest Update:Latest') {
                echo "triggering updatemanifestjob"
                build job: 'updatemanifest_001', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
        }
    
      }
