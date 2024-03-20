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
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }  
        stage("upload artifacts"){
            steps{
                 
                    nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: 'http://13.51.157.157:8081/',
                    groupId: 'QA',
                    version: "${env.BUILD_ID}-${env.BUILD_TIMESTAMP}",
                    repository: 'vprofile-release',
                    credentialsId: 'nexuslogin',
                    artifacts: [
                                [artifactId:'VProfile',
                                classifier: '',
                                file: "target/VProfile-1.0.war",
                                type: "war"]
                            ]
                     )
                    
                 
            }

        }
        
        
    }    
    
        }
