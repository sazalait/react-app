def pipelineName = "CICD for React-app"

pipeline {
    options { skipDefaultCheckout(true) }
    agent { label 'webserver' }

    environment {
        GIT_TRACE       = 'false'   // Trace git for testing  true/false,1,2
        GIT_TRACE_SETUP = 'true'    // really cool trace tools
        USS_WORKDIR        = "/u/jenkins/test/workspace"
        USS_WORKDIR_SCRIPT = "/u/jenkins/test/scripts"
        REPO_URL           = "https://github.com/sazalait/react-app.git"
        BRANCH             = "release"
    }

    stages {
        stage('Set Build Name') {
            steps {
                script {
                    currentBuild.displayName = "${pipelineName} - #${BUILD_NUMBER}"
                }
            }
        }

        stage('Cleanup') {
            steps {
                script {
                    echo "Cleaning up workspace: ${USS_WORKDIR}"
                    dir("${USS_WORKDIR_SCRIPT}") {
                        sh "./cleanup.sh ${USS_WORKDIR}"
                    }
                }
            }
        }

        stage('Git Clone') {
            steps {
                script {
                    echo "Cloning repository ${REPO_URL} (branch: ${BRANCH}) into ${USS_WORKDIR}"
                    dir("${USS_WORKDIR_SCRIPT}") {
                        sh "./gitclone.sh -w ${USS_WORKDIR} -r ${REPO_URL} -b ${BRANCH}"
                    }
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    echo "Running npm build inside ${USS_WORKDIR}"
                    dir("${USS_WORKDIR}") {   // Make workspace current dir
                        // Pass '.' to build.sh so it writes relative to workspace
                        sh "${USS_WORKDIR_SCRIPT}/build.sh ."
                    }
                }
            }
        }
    stage('Archive Reports') {
      steps {
         dir("${USS_WORKDIR}") {
            archiveArtifacts(
                artifacts: 'build-reports/*.log,build-reports/*.json,build-reports/*.html,build-reports/*.txt',
                excludes: '*clist',
                allowEmptyArchive: true,
                onlyIfSuccessful: false
            )
         }
     }
 }
        
    }
}
