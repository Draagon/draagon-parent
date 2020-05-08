pipeline {
    agent any
    options {
         timestamps()
    }
    stages {
        stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                '''
            }
        }
        stage ('Build') {
            steps {
                sh 'mvn clean package -Dmaven.test.failure.ignore=false'
            }
        }
        stage ('Deploy') {
            when {
                branch 'master'
            }
            steps {
                sh 'mvn deploy'
            }
        }

        stage("Release") {
            when {
                branch 'master'
            }
            steps {
                mvn 'release:prepare -Pnexus'
                mvn 'release:perform -Pnexus'
            }
        }
    }
}
