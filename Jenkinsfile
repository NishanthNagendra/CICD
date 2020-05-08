
pipeline {
   agent any

   stages {
      stage('checkout_Code_integration') {
         steps {
         	checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/NishanthNagendra/CICD']]])   
	 }
      }
      stage('Unit_Testing') {
         steps {
         	sh "/usr/local/bin/pip install -r requirements.txt"
            	sh "/usr/bin/python -m pytest -v tests/test_generator.py"
         }
      }
      stage('Docker_image_Build') {
         steps {

            sh "/usr/bin/docker build -t nishanth1998/cicd-example:latest ."

         }
      }
      stage('publish') {
         steps {
		withDockerRegistry(credentialsId: '7e490a13-d752-4773-8c35-b5591b1138f1', url: 'https://hub.docker.com/repository/docker/nishanth1998/cicd-example') {
                     sh "/usr/bin/docker push nishanth1998/cicd-example:latest"
         	}
         }
      }
      stage('Running_image_from_DockerHub') {
         steps {

           sh "/usr/bin/docker run -p 5000:5000 --rm nishanth1998/cicd-example:latest"
         }
         }
      }
   }
