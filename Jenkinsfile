//Declarative Pipeline
pipeline {
    agent {
    node {
        label 'master'
        //customWorkspace '/some/other/path'
    }
}
    stages {
        stage('parallel') {
        parallel {
            stage('build1') {
            steps {
                echo 'Hello World1'
            }
        }
        stage('build2') {
            steps {
                echo 'Hello World2'
            }
        }
        }
        }
  stage('run-parallel-branches') {
  steps {
    parallel(
      a: {
        echo "This is branch a"
      },
      b: {
        echo "This is branch b"
      }
    )
  }
}
        stage('test') {
            steps {
                catchError(buildResult: 'FAILURE', stageResult: 'FAILURE') {
                    sh "exit 1"
                }
            }
        }
        stage('deploy') {
            steps {
                script {
                try {
                    sh "exit 0"
                }
                catch(e) {
                    currentBuild.result = 'FAILURE'
                    throw e
                }
                }
            }
        }
        stage('review') {
            steps {
                echo 'Hello World'
            }
        }
    }
}
