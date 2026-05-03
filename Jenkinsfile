@Library("shared") _
pipeline {
    agent { label 'vinod'}
    stages {
        
        stage("code"){
            steps{
            echo "copying the code from Github"
            clone("https://github.com/chauhanvishal365/notes-app-k8s.git" ,'main')
            echo 'code clonned successfully'
            }
            
        }
        stage("build"){
            steps{
                echo 'building the code'
                
                sh 'docker build -t notesapp:latest .'
                
            }
        }
        stage("push"){
            steps{
                echo 'pushing the code to dockerHUb'
                sh "docker image tag notesapp:latest chauhanvishal365/notesapp:latest"
                withCredentials([usernamePassword(credentialsId: 'dockerhub-cred', 
                passwordVariable: 'DOCKER_PASS', usernameVariable: 'DOCKER_USER')]) { 
                sh "docker login -u \$DOCKER_USER -p \$DOCKER_PASS"
                sh "docker push chauhanvishal365/notesapp:latest"            
                    
                }
            }
            
        }
        stage("deploy"){
            steps{
                echo 'deploying the code'
            }
            
        }
    }
}
