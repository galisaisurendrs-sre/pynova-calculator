@Library("ci-shared-library") _

pipeline {
    agent any

    parameters {
        gitParameter(
            name: 'BRANCH_NAME',
            type: 'PT_BRANCH',
            defaultValue: 'main',
            branch: 'refs/heads/',
            selectedValue: 'DEFAULT',
            quickFilterEnabled: true,
            sortMode: 'DESCENDING',
            description: 'Select a Git branch to build',
            useRepository: 'git@github.com:galisaisurendrs-sre/pynova-calculator.git'
        )
    }

    stages {
        stage('Get Branch') {
            steps {
                script {
                    def branchName = params.BRANCH_NAME.replaceFirst(/^origin\//, '')
                    echo "User selected branch: ${branchName}"
                    env.SELECTED_BRANCH = branchName
                }
            }
        }

        stage('Clone Repository') {
            steps {
                script {
                    echo "Cloning branch: ${env.SELECTED_BRANCH}"

                    gitClone(
                        repo: 'git@github.com:galisaisurendrs-sre/pynova-calculator.git',
                        branch: env.SELECTED_BRANCH,
                        credsId: 'jenkins-key'
                    )
                }
            }
        }
    }
}