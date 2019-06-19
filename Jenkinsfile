pipeline{
           agent any
                triggers {
        cron('* * * * 1-5')
    }
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
                                          "pattern": "target/*.war",
                                          "target": "example-repo-local"
                                          }
                                          ]
                                          }"""
                                     )
                                  }
             
                       }
                       stage('Docker Deploy'){
                                  steps{
                                         sh 'wget http://13.67.56.156:8081/artifactory/example-repo-local/mavenwebApp.war'
                                         sh 'docker cp mavenwebApp.war aa9290ba1adc:/usr/local/tomcat/webapps/mavenwebApp.war'
                                    
                                     
                       }
            }
                       stage('remove old artifacts'){
                                  steps{
                                             sh 'rm -f mavenwebApp.war'
                                  }
                       }
            }
           
           }
              
                    
