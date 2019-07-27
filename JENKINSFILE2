pipeline {
    agent any


    stages {
        stage('SCM Checkout'){
          git 'https://github.com/prakashk0301/maven-project'
        }
  }
    {
        stage ('Compile Stage') {

            steps {
                withMaven(maven : 'JenkinsLocalMaven') {
                    sh 'mvn clean compile'
                }
            }
        }

        stage ('Testing Stage') {

            steps {
                withMaven(maven : 'JenkinsLocalMaven') {
                    sh 'mvn test'
                }
            }
        }


        stage ('install Stage') {
            steps {
                withMaven(maven : 'JenkinsLocalMaven') {
                    sh 'mvn install'
                }
            }
        }
        stage ('deploy to dev') {
             steps {
                  sshagent(['e58beaa6-b393-4e31-9d16-c509821c53ca']) {
                  sh 'scp -o StrictHostKeyChecking=no */target/*.war ec2-user@172.31.16.121:/var/lib/tomcat/webapps'
} } }

         
}
}
