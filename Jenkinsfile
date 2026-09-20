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

                        stage('Quality Gate') {
                            steps {
                                withSonarQubeEnv('local_sonarqube') {
                                    sh '''
                                        set -e

                                        REPORT_FILE="hello-world/target/sonar/report-task.txt"

                                        TASK_URL=$(awk -F= '$1=="ceTaskUrl"{print $2}' "$REPORT_FILE")

                                        echo "Ожидаем завершения анализа SonarQube..."

                                        for i in $(seq 1 60); do
                                            TASK_STATUS=$(curl -sS \
                                                -u "$SONAR_AUTH_TOKEN:" \
                                                "$TASK_URL" | jq -r '.task.status')

                                            echo "Статус анализа: $TASK_STATUS"

                                            if [ "$TASK_STATUS" = "SUCCESS" ]; then
                                                break
                                            fi

                                            if [ "$TASK_STATUS" = "FAILED" ] || [ "$TASK_STATUS" = "CANCELED" ]; then
                                                echo "Анализ SonarQube завершился с ошибкой"
                                                exit 1
                                            fi

                                            sleep 5
                                        done

                                        QUALITY_STATUS=$(curl -sS \
                                            -u "$SONAR_AUTH_TOKEN:" \
                                            "$SONAR_HOST_URL/api/qualitygates/project_status?projectKey=hello-world" \
                                            | jq -r '.projectStatus.status')

                                        echo "Quality Gate: $QUALITY_STATUS"

                                        if [ "$QUALITY_STATUS" != "OK" ]; then
                                            echo "Quality Gate не пройден!"
                                            exit 1
                                        fi

                                        echo "Quality Gate успешно пройден"
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
                                        -Dsonar.projectKey=hello-jenkins \
                                        -Dsonar.projectName="hello-jenkins"
                                    '''
                                }
                            }
                        }

                        stage('Quality Gate') {
                            steps {
                                withSonarQubeEnv('local_sonarqube') {
                                    sh '''
                                        set -e

                                        REPORT_FILE="hello-jenkins/target/sonar/report-task.txt"

                                        TASK_URL=$(awk -F= '$1=="ceTaskUrl"{print $2}' "$REPORT_FILE")

                                        echo "Ожидаем завершения анализа SonarQube..."

                                        for i in $(seq 1 60); do
                                            TASK_STATUS=$(curl -sS \
                                                -u "$SONAR_AUTH_TOKEN:" \
                                                "$TASK_URL" | jq -r '.task.status')

                                            echo "Статус анализа: $TASK_STATUS"

                                            if [ "$TASK_STATUS" = "SUCCESS" ]; then
                                                break
                                            fi

                                            if [ "$TASK_STATUS" = "FAILED" ] || [ "$TASK_STATUS" = "CANCELED" ]; then
                                                echo "Анализ SonarQube завершился с ошибкой"
                                                exit 1
                                            fi

                                            sleep 5
                                        done

                                        QUALITY_STATUS=$(curl -sS \
                                            -u "$SONAR_AUTH_TOKEN:" \
                                            "$SONAR_HOST_URL/api/qualitygates/project_status?projectKey=hello-jenkins" \
                                            | jq -r '.projectStatus.status')

                                        echo "Quality Gate: $QUALITY_STATUS"

                                        if [ "$QUALITY_STATUS" != "OK" ]; then
                                            echo "Quality Gate не пройден!"
                                            exit 1
                                        fi

                                        echo "Quality Gate успешно пройден"
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
                                        -Dsonar.projectKey=hello-devops \
                                        -Dsonar.projectName="hello-devops"
                                    '''
                                }
                            }
                        }

                        stage('Quality Gate') {
                            steps {
                                withSonarQubeEnv('local_sonarqube') {
                                    sh '''
                                        set -e

                                        REPORT_FILE="hello-devops/target/sonar/report-task.txt"

                                        TASK_URL=$(awk -F= '$1=="ceTaskUrl"{print $2}' "$REPORT_FILE")

                                        echo "Ожидаем завершения анализа SonarQube..."

                                        for i in $(seq 1 60); do
                                            TASK_STATUS=$(curl -sS \
                                                -u "$SONAR_AUTH_TOKEN:" \
                                                "$TASK_URL" | jq -r '.task.status')

                                            echo "Статус анализа: $TASK_STATUS"

                                            if [ "$TASK_STATUS" = "SUCCESS" ]; then
                                                break
                                            fi

                                            if [ "$TASK_STATUS" = "FAILED" ] || [ "$TASK_STATUS" = "CANCELED" ]; then
                                                echo "Анализ SonarQube завершился с ошибкой"
                                                exit 1
                                            fi

                                            sleep 5
                                        done

                                        QUALITY_STATUS=$(curl -sS \
                                            -u "$SONAR_AUTH_TOKEN:" \
                                            "$SONAR_HOST_URL/api/qualitygates/project_status?projectKey=hello-devops" \
                                            | jq -r '.projectStatus.status')

                                        echo "Quality Gate: $QUALITY_STATUS"

                                        if [ "$QUALITY_STATUS" != "OK" ]; then
                                            echo "Quality Gate не пройден!"
                                            exit 1
                                        fi

                                        echo "Quality Gate успешно пройден"
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
