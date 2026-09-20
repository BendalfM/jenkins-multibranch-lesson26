pipeline {
    agent {
        label 'maven'
    }

    stages {
        stage('Parallel Applications') {
            parallel {
                stage('Hello World') {
                    when {
                        changeset "hello-world/**"
                    }
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
                    when {
                        changeset "hello-jenkins/**"
                    }
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
                    when {
                        changeset "hello-devops/**"
                    }
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
