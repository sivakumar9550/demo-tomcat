pipeline{
    agent any 
    tools{
        maven 'maven-3'
    }
    stages{
        stage ('Build'){
            steps{
                sh 'mvn clean package'
            }
            post{
                success{
                    echo "Archiving the Artifacts"
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage ('Deploy to tomcat server') {
            steps{
                deploy adapters: [tomcat7(credentialsId: 'tomcat-cre', path: '', url: 'http://44.202.69.16:8080/')], contextPath: null, war: '**/*.war'
                echo "Deployment"
            }
        }
    }
}
