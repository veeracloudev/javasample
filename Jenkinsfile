pipeline{
    agent any
    tools{
        maven 'MAVEN'
    }
    stages{
        stage("git Checkout")
        {
           steps
            {
                 git url: 'https://github.com/veeracloudev/javasample.git', branch: 'main'
                 sh 'ls -l'
            }

        }
        stage("Build and generate artifact"){
            steps{
                sh 'mvn clean install'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }  
       

        }
        
        
    }    
    
        }
