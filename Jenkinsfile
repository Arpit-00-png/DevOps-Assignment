pipeline {
    agent any

    triggers {
        pollSCM('H/2 * * * *')
    }

    options {
        timestamps()
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Automated Tests') {
            steps {
                dir('task-api') {
                    sh './mvnw -B clean test'
                }
            }
        }

        stage('Build Application') {
            steps {
                dir('task-api') {
                    sh './mvnw -B package -DskipTests'
                }
            }
        }

        stage('Build Versioning') {
            steps {
                script {
                    def commitId = env.GIT_COMMIT.take(7)
                    def buildVersion = "1.0.${env.BUILD_NUMBER}-${commitId}"

                    dir('task-api') {
                        writeFile file: 'build-info.txt',
                            text: "Application: Task API\nBuild Version: ${buildVersion}\nGit Commit: ${env.GIT_COMMIT}\n"
                    }

                    echo "Generated Build Version: ${buildVersion}"
                }
            }
        }
    }

    post {
        success {
            echo 'Task API CI Pipeline completed successfully!'
            archiveArtifacts artifacts: 'task-api/target/*.jar, task-api/build-info.txt',
                             fingerprint: true
        }

        failure {
            echo 'CI Pipeline failed. Check the stage logs.'
        }
    }
}
