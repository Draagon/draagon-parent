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
              //timeout(time: 1, unit: 'MINUTES') {
                //input( message: 'Release to Central?', ok: 'Yes') //,
                                     //parameters: [booleanParam(defaultValue: true,
                                     //   description: 'If you want to perform a maven release, press yes',
                                     //   name: 'Yes?')])
                //if ( release ) {
                    //steps {
                    //      sh 'echo "Performing Release"'
            //            mvn 'release:prepare -Pnexus'
            //            mvn 'release:perform -Pnexus'
                    //}
                //}
                //input  {
                //    message 'Release to Central?'
                //}
                //steps {
                    sh 'echo "Performing Release"'
                    //mvn 'release:prepare -Pnexus'
                    //mvn 'release:perform -Pnexus'
                //}
              //}
            }
        }
    }
}
