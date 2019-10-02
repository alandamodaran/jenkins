pipeline {
  parameters {
    string(name: 'REPO', defaultValue:      'https://github.com/alandamodaran/helloWorld.git', description: 'Chart Repository')
    string(name: 'BRANCH', defaultValue:    'master', description: 'Repository Branch')
    string(name: 'APPLICATION', defaultValue: 'helloWorld', description: 'Name of the application to be deployed')
    string(name: 'TOMCATHOME', defaultValue:  '/root/apache-tomcat-9.0.26', description: 'Tomcat path where application to be deployed ')
  }
  agent any

  environment {
    // FOO will be available in entire pipeline
    FOO = "PIPELINE"
  }

  stages {
    stage("Checkout repo") {
      steps {
        sh "git clone --branch $BRANCH $REPO $APPLICATION";
        sh "pwd"
      }

    }
    stage("package") {
      steps {
        sh "cd $APPLICATION && mvn clean package"
      }
    }

    stage("upload to nexus") {
      steps {
        sh "echo deploy to  nexus -- to be developed"
      }
    }
    stage("Install in tomcat") {
      steps {
        //sh 'env > env.txt && cat env.txt'
        sh "echo install "
        sh "echo $WORKSPACE"
        sh "echo $PWD"
        sh "cp $WORKSPACE/$APPLICATION/target/hello.war  $TOMCATHOME/webapps"
        sh "sudo $TOMCATHOME/bin/shutdown.sh"
        //sleep command added so that all waiting threads be killed completely before starting the server 
        sh "/bin/sleep 30"
        sh "sudo $TOMCATHOME/bin/startup.sh"
      }
    }
    

  }
  post {
	always {
		cleanWs()
	}
   }
}
