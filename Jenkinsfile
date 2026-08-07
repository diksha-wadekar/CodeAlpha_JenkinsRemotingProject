// CodeAlpha DevOps Internship - Task 2: Jenkins Remoting Project
//
// This pipeline explicitly targets the remote agent node by label,
// proving the job executes on a distributed machine, not the controller.

pipeline {
    agent { label 'linux-remote' }

    options {
        timestamps()
    }

    stages {
        stage('Verify remote node') {
            steps {
                echo 'Running on remote Jenkins agent...'
                sh 'hostname'
                sh 'whoami'
                sh 'uname -a'
                sh 'pwd'
            }
        }

        stage('Simulate build work') {
            steps {
                echo 'Distributing a sample build task to the remote node'
                sh 'echo "Build started at $(date)"'
                sh 'mkdir -p build_output && echo "artifact content" > build_output/result.txt'
                sh 'cat build_output/result.txt'
            }
        }

        stage('Archive artifact') {
            steps {
                archiveArtifacts artifacts: 'build_output/*.txt', fingerprint: true
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished — check console output above to confirm it ran on remote-node-1.'
        }
        success {
            echo 'SUCCESS: job executed on the remote agent (see hostname output above).'
        }
        failure {
            echo 'FAILURE: check node connectivity / SSH credentials.'
        }
    }
}
