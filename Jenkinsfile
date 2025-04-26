pipeline {
    agent any  // Use any available agent/node

    environment {
        // Set environment variables if needed
        BUILD_ENV = 'dev'
    }

    parameters {
        string(name: 'RELEASE_VERSION', defaultValue: '1.0.0', description: 'Version to release')
        string(name: 'REPOSITORY', defaultValue: 'repo1,repo2', description: 'Comma-separated list of repositories')
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Checking out the code..."
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo "Starting build for release version: ${params.RELEASE_VERSION}"

                script {
                    def repos = params.REPOSITORY.tokenize(',')
                    for (repo in repos) {
                        echo "Building repository: ${repo}"
                        // Add your actual build commands here per repo
                        // Example: sh "cd ${repo} && make build"
                    }
                }
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                // sh 'make test' or any test script
            }
        }

        stage('Package') {
            steps {
                echo "Packaging artifacts for release version: ${params.RELEASE_VERSION}"
                // Example: sh 'tar -czf app.tar.gz build/'
            }
        }

        stage('Publish') {
            steps {
                echo "Publishing build artifacts..."
                // sh 'scp app.tar.gz user@server:/path/' or upload to S3/Nexus/etc.
            }
        }
    }

    post {
        success {
            echo 'Build completed successfully!'
        }
        failure {
            echo 'Build failed.'
        }
    }
}
