pipeline{

    agent any
    
    stages{

        stage("Git Clone"){
            
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/flavien-merlin/DevOps-Project.git']]])
            }
        }
        stage("Build"){

            steps{
                sh "docker-compose build"
            }
        }
        stage("Run"){

            steps{
                sh "docker-compose up -d"
            }
        }
        stage("Test"){

            steps{

                script{

                    try{
                        sh "python3 e2e.py"
                    }
                    catch(error){
                        sh "echo Jenkins failed"
                    }
                }
            }
        }
        
        stage("Finalize"){

            steps{
                sh "docker-compose push"
                sh "docker stop neo"
            }
        }
    }
    
}
