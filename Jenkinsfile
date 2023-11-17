pipeline {
    agent { label 'LABEL3' }
    triggers { pollSCM('* * * * *') }
    stages {
        stage('vcs') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/msteja143/MusicStore.git'
            }
        }
        stage('build') {
            steps {
                sh 'dotnet restore ./MusicStore/MusicStore.csproj dotnet build ./MusicStore/MusicStore.csproj'
            }
        }
        stage('test') {
            steps {
                sh 'dotnet test ./MusicStoreTest/MusicStoreTest.csproj dotnet test --logger "junit;LogFilePath=TEST-musicstoretest.xml"'
                sh 'dotnet test --logger "junit;LogFilePath=TEST-musicstoretest.xml" ./MusicStoreTest/MusicStoreTest.csproj'
                junit testResults: '**/TEST-*.xml'
            }
        }
    }
           post {
         success {
            mail subject: "Jenkins Build of ${JOB_NAME} with id ${BUILD_ID} is success",
                body: "Use this URL ${BUILD_URL} for more info",
                to: 'sandbox.smtp.mailtrap.io',
                from: 'tejaarts42@gmail.com'
        }
        failure {
            mail subject: "Jenkins Build of ${JOB_NAME} with id ${BUILD_ID} is failed",
                body: "Use this URL ${BUILD_URL} for more info",
                to: 'sandbox.smtp.mailtrap.io',
                from: 'tejaarts42@gmail.com'
                 }
              }
}