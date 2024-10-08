node{
    def mavenHome = tool name: 'maven3.9.8'
    stage('1CloneCode'){
        git "https://github.com/nfestaclass04/maven-web-application.git"
    }
    stage('2Test&Build'){
        sh "${mavenHome}/bin/mvn install"
    }
    /*
    stage('3CodeQuality'){
        sh "${mavenHome}/bin/mvn sonar:sonar"
    }
    */
    stage('4UploadArtifacts'){
        sh "${mavenHome}/bin/mvn deploy"
    }
    stage('5DeploymentToUat'){
        deploy adapters: [tomcat9(credentialsId: 'jenkins-tomcat-creds', path: '', url: 'http://3.236.174.60:8080/')], contextPath: null, war: 'target/*war'
    }
    stage('6Approval'){
        timeout(time:11, unit:'HOURS'){
            input message: 'Application is now ready for deployment to production. Please, review and provide your Approval'
        }
    }
    stage('7DeploymentToProd'){
        deploy adapters: [tomcat9(credentialsId: 'jenkins-tomcat-creds', path: '', url: 'http://44.197.229.164:8080/')], contextPath: null, war: 'target/*war'
    }
    stage('8Notifications'){
        emailext body: '''This would be the final status report on pipeline builds.

Regards
''', subject: 'Pipeline Status', to: 'nfestatech@mail.com'
    }
}
