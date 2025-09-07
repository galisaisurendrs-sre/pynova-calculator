@Library("ci-shared-library") _

pipeline {
    agent any

    parameters {
        gitParameter(
            name: 'BRANCH_NAME',
            type: 'PT_BRANCH',
            defaultValue: 'main',
            branch: '',
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
                    // Strip 'origin/' prefix if present
                    def branchName = params.BRANCH_NAME.replaceFirst(/^origin\//, '')
                    echo "User selected branch: ${branchName}"

                    // Save branch name for downstream stages
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