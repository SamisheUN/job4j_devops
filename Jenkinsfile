pipeline {
    agent {
        label 'agent1'
    }

    tools {
        git 'Default'
    }

    stages {
        stage('Prepare') {
            steps {
    sh 'chmod +x gradlew'
    sh './gradlew build'
}
        }
        stage('Parallel Build') {
            parallel {

                stage('Checkstyle Main') {
                    steps {
                        sh './gradlew checkstyleMain'
                    }
                }

                stage('Checkstyle Test') {
                    steps {
                        sh './gradlew checkstyleTest'
                    }
                }
                stage('Build') {
                    steps {
                        sh './gradlew build'
                    }
                }
                stage('Test and JaCoCo') {
                    steps {
                        sh './gradlew test'
                        sh './gradlew jacocoTestReport'
                        sh './gradlew jacocoTestCoverageVerification'
                    }
                }
            }
        }
    }
}
