pipeline {
    agent any
    triggers {
        cron(' H/15 * * * * ')
     }
    tools {
        maven 'M2_HOME'
      
    }
    stages {
      stage('Build'){
        steps {
          echo "Build steps"
          sh 'mvn clean'
          sh 'mvn install'
          sh 'mvn package'
        }
      
      
      }
        stage('test '){
        steps {
            retry(4){
          echo  "test step"
         
            }
          sh 'mvn test'
        }
      
      
      }
        stage('deploy'){
        steps {
         
         sshPublisher(publishers: [sshPublisherDesc(configName: 'Docker-host', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'docker build -t eab046/pcontact:v.${BUILD_NUMBER} .; docker tag eab046/pcontact:v.${BUILD_NUMBER} eab046/pcontact:v.${BUILD_NUMBER}; docker push eab046/pcontact:v.${BUILD_NUMBER} ', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '/webapp/target', sourceFiles: '**/*.war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
                   
        }
      
      
      }
    
    }
    post {
        always {
            echo "Always display this message "
        }
        failure {
            echo "Job failed "
        }
        success {
            echo "Successful run "
        }
        unstable {
            echo "The job is unstable "
        }
    } 

}
