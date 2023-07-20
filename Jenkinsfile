#!groovy
pipeline {
    agent any
    stages {

        stage('Git checkout') {
            steps {
                git 'https://github.com/Antonppavlov/jmeter-jenkins.git'
            }
        }

        stage('Start Performance Tests') {
            steps {
                withMaven(maven: 'maven 3.9.3') {
                    sh '''
                        mvn clean verify -DjmeterScript=jmeter_start_in_jenkins.jmx
                    '''
                }
            }
        }

        stage('Publish Performance test result report') {
            steps {
                perfReport filterRegex: '',
                        showTrendGraphs: true,
                        sourceDataFiles: 'target/jmeter/results/jmeter_start_in_jenkins.jtl'
            }
        }

    }
}