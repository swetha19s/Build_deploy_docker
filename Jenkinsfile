pipeline{
           agent any
          
            stages{
                   stage('code checkout'){
                     steps{
                          git url:'https://github.com/swetha19s/Docker_pipeline.git',branch:'master'
                          }
                        }
                       stage('maven'){
                           steps{
                                  sh ' mvn clean install'
                                            }
                                 }
                       stage('Upload artifacts'){
                                  steps{
                                    rtUpload (
                                          serverId: "Artifactory",
                                          spec:
                                          """{
                                          "files": [
                                          {
                                          "pattern": "/var/lib/jenkins/workspace/Build_deploy_docker/target/*.war",
                                          "target": "example-repo-local"
                                          }
                                          ]
                                          }"""
                                     )
                                  }
             
                       }
                       stage('Docker Deploy'){
                                  steps{
                                         sh ' wget http://13.67.56.156:8081/artifactory/example-repo-local/mavenwebApp.war -o /var/lib/jenkins/workspace/Build_deploy_docker/mavenwebApp.war'
                                         sh 'docker cp /var/lib/jenkins/workspace/Build_deploy_docker/mavenwebApp.war aa9290ba1adc:/usr/local/tomcat/webapps/mavenwebApp.war'
                                     
                       }
            }
            }
           
           }
              
                    
