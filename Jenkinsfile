pipeline {
    agent { label 'win' }  

    stages {
        stage('Checkout') {
            steps {
                echo 'Using Jenkins SCM checkout...'
                bat 'dir' 
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies...'
                bat 'python -m pip install --upgrade pip'
                bat 'pip install -r requirements.txt'
            }
        }

        stage('Verify Files') {
            steps {
                echo 'Listing files in workspace...'
                bat 'dir'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                bat 'pytest --maxfail=1 --disable-warnings -q --junitxml=report.xml'
            }
        }

        stage('Archive Results') {
            steps {
                echo 'Archiving test results...'
                archiveArtifacts artifacts: '**/report.xml', fingerprint: true, allowEmptyArchive: true
                junit 'report.xml'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully '
        }
        failure {
            echo 'Pipeline failed '
        }
    }
}
