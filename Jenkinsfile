pipeline {
    agent { docker 'golang:1.19' }

    stages {
        stage('Test') {
            steps {
                sh 'go test ./...'
            }
        }

        stage('Build Image') {
            steps {
                script {
                    def imageName = tapBuildImage(destination: 'gcr.io/org/name', context: '.')
                }
            }
        }

        stage('Scan Image') {
            steps {
                tapScanImage(image: imageName)
            }
        }

        stage('Build PodSpec') {
            steps {
                tapBuildPodSpec(image: imageName)
            }    
        }
    }
}
