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
        boolean release = false
        when {
            branch 'master'
        }
        stage("Release confirmation") {
            timeout(time: 1, unit: 'MINUTES') {
                input 'Release to Central?'
                release = true
            }
        }
        if (release) {
            stage("Release") {
                mvn 'release:prepare -Pnexus'
                mvn 'release:perform -Pnexus'
            }
        }
    }
}
