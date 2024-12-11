pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                 git url: 'https://github.com/Cvoluj/sp_lab4.git', branch:'main', credentialsId: 'jenkins'
            }
        }
        
        stage('Build') {
            steps {
                bat '"C:\\Program Files\\Microsoft Visual Studio\\2022\\Community\\MSBuild\\Current\\Bin\\MSBuild.exe" test_repos.sln /t:Build /p:Configuration=Release'
            }
        }

        stage('Test') {
            steps {
                bat "x64\\Debug\\test_repos.exe --gtest_output=xml:test_report.xml"
            }
        }
    }

    post {
    always {
        // Publish test results using the junit step
        // Specify the path to the XML test result files
        junit '**/test_report.xml'
    }
}
}