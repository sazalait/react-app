pipeline {
    agent { label 'webserver' }

    environment {
        USS_WORKDIR        = "/u/jenkins/test/workspace"
        USS_WORKDIR_SCRIPT = "/u/jenkins/test/scripts"
        REPO_URL           = "https://github.com/sazalait/react-app.git"
        BRANCH             = "main"
    }

    stages {
        stage('Cleanup') {
            steps {
                script {
                    echo "Cleaning up workspace: ${USS_WORKDIR}"
                    dir(USS_WORKDIR_SCRIPT) {
                        sh "./cleanup.sh ${USS_WORKDIR}"
                    }
                }
            }
        }

        stage('Git Clone') {
            steps {
                script {
                    echo "Cloning repository ${REPO_URL} (branch: ${BRANCH}) into ${USS_WORKDIR}"
                    dir(USS_WORKDIR_SCRIPT) {
                        sh "./gitclone.sh -w ${USS_WORKDIR} -r ${REPO_URL} -b ${BRANCH}"
                    }
                }
            }
        }

stage('Build') {
    steps {
        script {
            echo "Running npm build inside ${USS_WORKDIR}"
            dir("${USS_WORKDIR_SCRIPT}") {
                sh "./build.sh ${USS_WORKDIR}"
            }
        }
    }
}
    }
    post {
        always {
            archiveArtifacts artifacts: "build-reports/*.txt", onlyIfSuccessful: false
        }
    }
}
