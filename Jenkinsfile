pipeline {
    agent any

    environment {
        GITHUB_TOKEN = credentials('github-token')
        GITHUB_REPO = 'cyse7125-su24-team13/k8s-yaml-manifests'
        GITHUB_API_URL = 'https://api.github.com'
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    def scmVars = checkout scm
                    def commitId = scmVars.GIT_COMMIT
                    env.GIT_COMMIT_ID = commitId
                }
            }
        }
        stage('Run yamllint') {
            steps {
                // Run yamllint on the repository
                sh '''
                    yamllint .
                '''
            }
        }
    }

    post {
        success {
            script {
                def commitId = env.GIT_COMMIT_ID
                def status = 'success'
                def description = 'yamllint successful.'
                notifyGithub(commitId, status, description)
            }
        }

        failure {
            script {
                def commitId = env.GIT_COMMIT_ID
                def status = 'failure'
                def description = 'yamllint failed.'
                notifyGithub(commitId, status, description)
            }
        }
    }
}

def notifyGithub(commitId, status, description) {
    def context = 'Terraform'
    def url = "${env.GITHUB_API_URL}/repos/${env.GITHUB_REPO}/statuses/${commitId}"

    def payload = [
        state: status,
        target_url: env.BUILD_URL,
        description: description,
        context: context
    ]

    def response = sh(
        script: """#!/bin/bash
        curl -s -H "Authorization: token ${env.GITHUB_TOKEN}" \\
             -H "Content-Type: application/json" \\
             -d '${groovy.json.JsonOutput.toJson(payload)}' \\
             ${url}
        """,
        returnStdout: true
    ).trim()

    echo "GitHub API response: ${response}"
}
