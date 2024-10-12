node{
    def mavenHome = tool name: 'maven3.9.8'
    stage('1CloneCode'){
    //    git "https://github.com/nfestaclass04/maven-web-application.git"
        git branch: 'bug-fix', url: 'https://github.com/yaseen-13/my-test-jk-app.git'
    }
    
    stage('2Test&Build'){
        sh "${mavenHome}/bin/mvn clean install"
   }
   
   stage('3UploadArtifacts'){
        sh "${mavenHome}/bin/mvn deploy"
    }
    
    stage('5DeploymentToUat'){
        deploy adapters: [tomcat9(credentialsId: 'tomcat-jenkins-0', path: '', url: 'http://18.188.198.25:8080/')], contextPath: null, war: 'target/*war'
    }
    /*
    stage('6Approval'){
        timeout(time:11, unit:'HOURS'){
            input message: 'Application is now ready for deployment to production. Please, review and provide your Approval'
        }
    }
    
    
    stage('7DeploymentToProd'){
        deploy adapters: [tomcat9(credentialsId: 'tomcat-cred', path: '', url: 'http://3.128.34.244:8080/')], contextPath: null, war: 'target/*war'
    }
    */
}

   
