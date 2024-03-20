pipeline{
    agent any
    tools{
        jdk 'jdk8'
        maven 'MAVEN3'
        
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
        }   
        
        
    }    
    
        }
