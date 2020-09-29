pipeline {
    environment {
    registry = "priya2802/gitfocus_service_kube"
    registryCredential = 'GITFocus-DockerHub'
    dockerImage = ''
  }
    agent {
        docker { image 'node:10-alpine' }
    }
    stages {
        stage('Restore') {
            steps {
                sh 'npm install'
                sh 'cp  index.d.ts ./node_modules/@types/chart.js'
            }
        }
        stage('Build') {
            steps {
                sh 'npm run-script build'
            }
        }
        stage('Clean Up'){
            steps {
                sh 'rm -r src output  e2e'
                sh 'rm -f browserslist tsconfig.app.json README.md package-lock.json  tsconfig.json angular.json  tsconfig.spec.json karma.conf.js  tslint.json index.d.ts package.json'
            }
        }
        stage('Building Image') {
            dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }        
        /*stage('Deploy') {
            steps {
                sh 'rm ../../apps/*'
                sh 'cp ./dist/apps/* ../../apps/'
            }*/
        }            
    }
}
