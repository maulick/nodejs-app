pipeline {
    agent any
    tools {
      nodejs '20.7.0'
    }
    stages {
        stage('print versions') {
          steps {
            sh 'npm version'
          }
        }
        stage('Install') {
      steps {
        sh 'npm install'
      }
        }
        stage('Build') {
      steps {
        sh 'npm run build'
      }
        }
        stage('Code Deploy to EC2') {
          steps {
            step(
              [
                $class: 'AWSCodeDeployPublisher',
                applicationName: 'nodejs-app',
                deploymentGroupAppspec: false,
                deploymentGroupName: 'nodejs-app-deploy-grp',
                excludes: '',
                iamRoleArn: '',
                includes: 'dist/',
                proxyHost: '',
                proxyPort: 0,
                region: 'ap-south-1',
                s3bucket: 'deploymasters-node',
                s3prefix: '',
                subdirectory: '',
                versionFileName: '',
                waitForCompletion: false
                ]
              )
          }
        }
    }
}
