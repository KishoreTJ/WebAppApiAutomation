pipeline {
  agent any
  stages {
    stage('Dev-Build') {
      steps {
        git(url: 'https://github.com/KishoreTJ/WebApp.git', branch: 'master', poll: true)
        bat 'mvn install'
        bat 'Set JENKINS_NODE_COOKIE=dontKillMe && start /min startApp.bat'
        bat 'stopApp.bat'
      }
    }

    stage('QA UI Automation') {
      parallel {
        stage('QA UI Automation') {
          steps {
            git(url: 'https://github.com/KishoreTJ/WebAppUiAutomation.git', branch: 'master')
            bat 'mvn test'
          }
        }

        stage('QA API Automation') {
          steps {
            git 'https://github.com/KishoreTJ/WebAppApiAutomation'
            bat 'mvn test'
          }
        }

      }
    }

  }
}