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
                                sh 'java -cp hello-world/target/classes com.example.HelloWorld'
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
                                sh 'java -cp hello-jenkins/target/classes com.example.HelloJenkins'
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
                                sh 'java -cp hello-devops/target/classes com.example.HelloDevops'
                            }
                        }
                    }
                }
            }
        }
    }
}
