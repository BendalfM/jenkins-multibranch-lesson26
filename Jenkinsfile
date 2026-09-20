pipeline {
    agent {
        label 'maven'
    }

    stages {
        stage('Parallel Applications') {
            parallel {
                stage('Hello World') {
                    stages {
                        stage('Build') {
                            steps {
                                sh 'mvn -f hello-world/pom.xml clean package'
                            }
                        }

                        stage('Test') {
                            steps {
                                sh 'mvn -f hello-world/pom.xml test'
                            }
                        }

                        stage('Deploy') {
                            steps {
                                sh 'java -jar hello-world/target/hello-world-1.0.jar'
                            }
                        }
                    }
                }

                stage('Hello Jenkins') {
                    stages {
                        stage('Build') {
                            steps {
                                sh 'mvn -f hello-jenkins/pom.xml clean package'
                            }
                        }

                        stage('Test') {
                            steps {
                                sh 'mvn -f hello-jenkins/pom.xml test'
                            }
                        }

                        stage('Deploy') {
                            steps {
                                sh 'java -jar hello-jenkins/target/hello-jenkins-1.0.jar'
                            }
                        }
                    }
                }

                stage('Hello Devops') {
                    stages {
                        stage('Build') {
                            steps {
                                sh 'mvn -f hello-devops/pom.xml clean package'
                            }
                        }

                        stage('Test') {
                            steps {
                                sh 'mvn -f hello-devops/pom.xml test'
                            }
                        }

                        stage('Deploy') {
                            steps {
                                sh 'java -jar hello-devops/target/hello-devops-1.0.jar'
                            }
                        }
                    }
                }
            }
        }
    }
}
