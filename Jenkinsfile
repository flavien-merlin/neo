pipeline {
    
    agent any

    stage("clone"){
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/flavien-merlin/DevOps-Project.git']]])
    }
    stage("Build"){
        sh "docker-compose build"
    }
    stage("Run"){
        sh "docker-compose up -d"
    }
    stage("Test"){
        try{
            sh "python3 e2e.py"
        }
        catch (error){
            sh "echo Jenkins failed"
        }
    }
    stage("Finalize"){
        sh "docker-compose push"
        sh "docker stop neo"
    }
}
