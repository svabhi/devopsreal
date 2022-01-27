pipeline {
    agent { label 'jdk11-mvn3.8.4' }
     options {
    buildDiscarder(logRotator(numToKeepStr: '2', artifactNumToKeepStr: '2'))
  }
    // triggers { 
    //     cron('5 * * * *')
    //     pollSCM('*/5 * * * *')
    // }
    parameters {
        string(name: 'MAVEN_GOAL', defaultValue: 'package', description: 'This is maven goal' )
        choice(name: 'BRANCH_TO_BUILD', choices: ['declarative', 'master', 'scripted'], description: 'Branch to build')
    }
    stages {
        stage('scm') {
            steps {
          
                git url: 'https://github.com/GitPracticeRepo/java11-examples.git', branch: "${params.BRANCH_TO_BUILD}"
            }
        }
        stage('build') {
            steps {
             
                sh "/usr/local/apache-maven-3.8.4/bin/mvn ${params.MAVEN_GOAL}"
            }
        }
    }
}