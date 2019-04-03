pipeline {
  agent any

  environment {
    COMMIT_MESSAGE = """${sh(
      returnStdout: true,
      script: "git --no-pager log --format='medium' -1 ${GIT_COMMIT}"
    )}"""

    GALAXY_REPO = "vermilion-tech ansible-role-docker4wordpress"
  }

  stages {
    stage('Notify Slack') {
      steps {
        slackSend(color: '#000000', message: "Build Started - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)\n```${env.COMMIT_MESSAGE}```")
      }
    }

    stage('Lint Ansible Role') {
      agent { docker { image 'williamyeh/ansible:ubuntu18.04'} }
      steps {
        sh 'pip install ansible-lint'
        script {
          LINT_OUTPUT = sh(script: "ansible-lint . || true", returnStdout: true)
        }
        slackSend(color: '#e987f1', message: "Ansible Lint\n```\n${LINT_OUTPUT}\n```")
      }
    }

    stage('Import Ansible Role') {
      when {
        anyOf {
          branch 'master';
          branch 'development'
        }
      }
      agent { docker { image 'williamyeh/ansible:ubuntu18.04'} }
      steps {
        withCredentials([string(credentialsId: "ansible-galaxy-pat", variable: "GITHUB_PAT")]) {
          sh 'ansible-galaxy login --github-token $GITHUB_PAT'
          script {
            IMPORT_OUTPUT = sh(script: "ansible-galaxy import --branch ${GIT_BRANCH} ${GALAXY_REPO}", returnStdout: true)
          }
        }
        slackSend(color: '#d577dd', message: "Ansible-Galaxy Role Imported\n```${IMPORT_OUTPUT}```")
      }
    }
  }

  post {
    failure {
      slackSend (color: '#FF0000', message: "Build Failed! - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)")
    }

    success {
      slackSend (color: '#00FF00', message: "Success! - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)")
    }
  }
}
