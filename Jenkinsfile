pipeline {
    agent {
        label 'agent1'
    }

    tools {
        git 'Default'
    }

    stages {
        stage('Build') {
            parallel {
                stage('Prepare Environment') {
                    steps {
                        script {
                            sh 'chmod +x ./gradlew'
                        }
                    }
                }
                stage('Checkstyle') {
                    parallel {
                        stage('Checkstyle Main') {
                            steps {
                                script {
                                    sh './gradlew checkstyleMain'
                                }
                            }
                        }
                        stage('Checkstyle Test') {
                            steps {
                                script {
                                    sh './gradlew checkstyleTest'
                                }
                            }
                        }
                        stage('Compile') {
                            steps {
                                sh './gradlew compileJava'
                            }
                        }
                        stage('Test') {
                            steps {
                                script {
                                    sh './gradlew test'
                                }
                            }
                        }
                        stage('JaCoCo') {
                            parallel {
                                stage('JaCoCo Report') {
                                    steps {
                                        script {
                                            sh './gradlew jacocoTestReport'
                                        }
                                    }
                                }
                                stage('JaCoCo Verification') {
                                    steps {
                                        script {
                                            sh './gradlew jacocoTestCoverageVerification'
                                        }
                                    }
                                }
                            }
                        }
                    }
                }
            }
        }


    }
}
