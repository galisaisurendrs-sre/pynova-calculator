@Library("ci-shared-library") _

pipeline {
    agent any

    stages {
        stage('Get Branch') {
            steps {
                script {
                    BRANCH_NAME = input(
                        id: 'userInput',
                        message: 'Enter Git branch to checkout',
                        parameters: [
                            string(defaultValue: 'main', description: 'Branch name', name: 'branch')
                        ]
                    )
                    echo "User selected branch: ${BRANCH_NAME}"
                }
            }
        }

        stage('Clone Repository') {
            steps {
                script {
                    gitClone(
                        'git@github.com:galisaisurendrs-sre/pynova-calculator.git',
                        BRANCH_NAME,
                        'jenkins-key'
                    )
                }
            }
        }
    }
}
