pipeline {
  agent any

  stages {
      stage('Clean WS') {
         steps {
                cleanWs()
         }
      }

      stage('Git clone') {
         steps {
               git branch: 'main', url: "https://github.com/meramsformations/petclinic.git"
         }
      }

      stage('Maven build') {
         steps {
                 sh "/opt/maven/bin/mvn clean package"
        }
      }

       stage('Prepare Files') {
         steps {
               sh "sed -i \"s/PKG_VERSION/${BUILD_NUMBER}/g\" deployit-petclinic.xml"
         }
      }

      stage('Publish XLDeploy Package') {
         steps {
               xldCreatePackage artifactsPath: '', darPath: 'petclinic-${BUILD_NUMBER}.dar', manifestPath: 'deployit-petclinic.xml'
               xldPublishPackage darPath: 'petclinic-${BUILD_NUMBER}.dar', serverCredentials: 'xl deploy'
         }//End steps
      }//End stage
  }//End stages
}//End pipeline

 
