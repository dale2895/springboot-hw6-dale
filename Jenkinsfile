pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/dale2895/springboot-hw6-dale.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh './mvnw clean package'
            }
        }

        stage('Upload JAR to Nexus') {
            steps {
                sh '''
                JAR_FILE=target/spring-boot-complete-0.0.1-SNAPSHOT.jar

                curl -v -u admin:admin123 --upload-file $JAR_FILE \
                "http://localhost:8081/repository/maven-releases/com/example/springboot/spring-boot-complete/0.0.1-SNAPSHOT/spring-boot-complete-0.0.1-SNAPSHOT.jar"
                '''
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }
}


