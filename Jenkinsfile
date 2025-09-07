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
                echo "User selected branch: ${params.BRANCH_NAME}"
            }
        }

        stage('Clone Repository') {
            steps {
                script {
                    gitClone(
                        'git@github.com:galisaisurendrs-sre/pynova-calculator.git',
                        params.BRANCH_NAME,
                        'jenkins-key'
                    )
                }
            }
        }
    }
}
