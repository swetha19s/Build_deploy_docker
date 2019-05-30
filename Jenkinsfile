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
                                          "pattern": "/var/lib/jenkins/workspace/Docker_build_deploy/target/*.war",
                                          "target": "example-repo-local"
                                          }
                                          ]
                                          }"""
                                     )
                                  }
             
                       }
                       stage('Docker Deploy'){
                                  steps{
                                         sh 'wget http://13.67.56.156:8081/artifactory/example-repo-local/mavenwebApp.war -o ./downloads/mavenwebApp.war'
                                         sh 'docker cp ./downloads/mavenwebApp.war aa9290ba1adc:/usr/local/tomcat/webapps/mavenwebApp.war'
                                         sh 'rm -f ./downloads/mavenwebApp.war'
                                     
                       }
            }
            }
           
           }
              
                    
