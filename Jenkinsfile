pipeline {

    agent any

    stages {

        stage('Build'){
            steps {
                sh "mvn clean"

                sh "mvn compile"
            }
        }

        stage('Test'){
            steps {
                sh "mvn test"
            }

            post {
                always {
                    junit '**/target/surefire-reports/TEST-*.xml'
                }
            }
        }

        stage('sonar scan'){
            steps {
              sh "mvn clean verify sonar:sonar \
  -Dsonar.projectKey=Abdulaziz_Aldossari \
  -Dsonar.host.url=http://54.226.50.200 \
  -Dsonar.login=sqp_33ced7f290e48592ae0d1787233c86e4e03885f2"
            }
        }

        stage('Package'){
            steps {

                sh "mvn package"
            }
            post {
                success {
                    archiveArtifacts artifacts: '**/target/*.war', followSymlinks: false
                }
            }
        }

    }

}
