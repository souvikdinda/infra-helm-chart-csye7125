pipeline {
    agent any
    
    stages{
        stage('Checkout Main Branch'){
            steps{
                script {
                    checkout([
                        $class: 'GitSCM',
                        branches: [[name: 'main']],
                        userRemoteConfigs: [[credentialsId: 'github_token', url: 'https://github.com/csye7125-fall2023-group07/infra-helm-chart.git']]
                    ])
                }
            }
        }

        stage('Semantic-Release') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'github_token', usernameVariable: 'GH_USERNAME', passwordVariable: 'GH_TOKEN')]) {
                        env.GIT_LOCAL_BRANCH = 'main'
                        def releaseOutput = sh(script: 'npx semantic-release --dry-run --json', returnStdout: true).trim()
                        def versionLine = releaseOutput.find(/Published release (\d+\.\d+\.\d+) on default channel/)

                        if(versionLine) {
                            def newVersion = (versionLine =~ /(\d+\.\d+\.\d+)/)[0][0]
                            echo "New version: v${newVersion}"
                            sh "helm package --version ${newVersion} ."
                            sh "gh release create 'v${newVersion}' *${newVersion}.tgz"
                            sh 'rm *.tgz'
                        } else {
                            error "Failed to capture the new version from semantic-release."
                        }
                    }
                }
            }
        }
    }

    post {
        success {
            build job: 'infra-helm-chart-deployment', wait: false
        }
    }
}