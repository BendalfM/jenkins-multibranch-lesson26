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
                        stage('SonarQube Analysis') {
                            steps {
                                withSonarQubeEnv('local_sonarqube') {
                                    sh '''
                                        mvn -f hello-world/pom.xml \
                                        org.sonarsource.scanner.maven:sonar-maven-plugin:sonar \
                                        -Dsonar.projectKey=hello-world \
                                        -Dsonar.projectName="Hello World"
                                    '''
                                }
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

                        stage('SonarQube Analysis') {
                            steps {
                                withSonarQubeEnv('local_sonarqube') {
                                    sh '''
                                        mvn -f hello-jenkins/pom.xml \
                                        org.sonarsource.scanner.maven:sonar-maven-plugin:sonar \
                                        -Dsonar.projectKey=hello-world \
                                        -Dsonar.projectName="Hello World"
                                    '''
                                }
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

                        stage('SonarQube Analysis') {
                            steps {
                                withSonarQubeEnv('local_sonarqube') {
                                    sh '''
                                        mvn -f hello-devops/pom.xml \
                                        org.sonarsource.scanner.maven:sonar-maven-plugin:sonar \
                                        -Dsonar.projectKey=hello-world \
                                        -Dsonar.projectName="Hello World"
                                    '''
                                }
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
