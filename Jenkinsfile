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
                                          "pattern": "/var/lib/jenkins/workspace/artifactory/target/*.war",
                                          "target": "example-repo-local"
                                          }
                                          ]
                                          }"""
                                     )
                                  }
             
                       }
                       stage('Docker Deploy'){
                                  steps{
                                     sh 'docker exec -i aa9290ba1adc /bin/bash'
                                     sh ' wget http://13.67.56.156:8081/artifactory/example-repo-local/mavenwebApp.war -o /usr/local/tomcat/webapps/mavenwebApp.war'
                       }
            }
            }
           
           }
              
                    
