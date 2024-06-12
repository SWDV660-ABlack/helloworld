#!groovy

node {
    stage('Checkout') {
        checkout scm
    }

    stage('Setup') {
        sh 'npm config set registry http://registry.npmjs.org/'
        sh 'npm install'
    }

    stage('Mocha test') {
        sh './node_modules/mocha/bin/mocha.js --exit test/helloworld_test.js'
    }

    stage('Cleanup') {
        echo 'Starting cleanup'
        try {
            sh 'npm prune'
            echo 'Prune completed'
            sh 'rm -rf node_modules'
            echo 'Node modules deleted'
        } catch (Exception e) {
            echo "Cleanup failed: ${e.message}"
        }
        echo 'Cleanup stage completed'
    }
}
