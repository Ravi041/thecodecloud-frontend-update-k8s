pipeline {
   agent any

    stages {
        stage('Git Checkout') {
            steps {
            script{
                git branch: 'main', credentialsId: 'GitHub', url: 'https://github.com/Ravi041/thecodecloud-frontend-update-k8s.git'  
                }  
            }
        }
        stage('Update Manifest'){
            steps {
            script{
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    //withCredentials([gitUsernamePassword(credentialsId: 'github', gitToolName: 'Default')]) {
   
                    withCredentials([usernamePassword(credentialsId: 'GitHub', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email ravindrak041@gmail.com"
                        sh "git config user.name ravindra"
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+416496057868.dkr.ecr.us-east-1.amazonaws.com/thecodecloud-frontend.*+416496057868.dkr.ecr.us-east-1.amazonaws.com/thecodecloud-frontend:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push --force https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/thecodecloud-frontend-update-k8s HEAD:main"
                        //sh "git push https://github.com/srikanta1219/update-k8s-manifest.git"
                        
                    }
                }
            }
        }    
            
    }
  
   }
}