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
                 script {
                    pom = readMavenPom file: "pom.xml";
                    filesByGlob = findFiles(glob: "target/*.${pom.packaging}");
                    echo "${filesByGlob[0].name} ${filesByGlob[0].path} ${filesByGlob[0].directory} ${filesByGlob[0].length} ${filesByGlob[0].lastModified}"
                    artifactPath = filesByGlob[0].path;
                    artifactExists = fileExists artifactPath;
                    if(artifactExists) {
                        echo "*** File: ${artifactPath}, group: ${pom.groupId}, packaging: ${pom.packaging}, version ${pom.version} ARTVERSION";
                    nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: 'http://13.51.157.157:8081/',
                    groupId: 'QA',
                    version: "${env.BUILD_ID}-${env.BUILD_TIMESTAMP}",
                    repository: 'project-release',
                    credentialsId: 'nexuslogin',
                    artifacts: [
                                [artifactId: pom.artifactId,
                                classifier: '',
                                file: artifactPath,
                                type: pom.packaging],
                                [artifactId: pom.artifactId,
                                classifier: '',
                                file: "pom.xml",
                                type: "pom"]
                            ]
                     );
                    }
                 }
            }

        }
        
        
    }    
    
        }
