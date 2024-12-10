pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                 git url: 'git@github.com:Cvoluj/sp_lab4.git', branch:'main', credentialsId: 'da81e558-3e4f-4807-83d8-c544dac30f90'
            }
        }
        
        stage('Build') {
            steps {
                // Крок для збірки проекту з Visual Studio
                // Встановіть правильні шляхи до рішення/проекту та параметри MSBuild
                sh './msbuild/Current/Bin/MSBuild.exe test_repos.sln /t:Build /p:Configuration=Release'
            }
        }

        stage('Test') {
            steps {
                // Команди для запуску тестів
                sh './x64/Debug/test_repos.exe --gtest_output=xml:test_report.xml'
            }
        }
    }

    post {
    always {
        // Publish test results using the junit step
        // Specify the path to the XML test result files
        junit 'test_report.xml'
    }
}
}