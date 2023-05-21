pipeline{
    
    agent any 
    
    stages {
        
        stage('Git Checkout'){
            
            steps{
                
                script{
                    
                    git branch: 'devops', url: 'https://github.com/akhilvijay15/nexus_helm_cicd_app.git'
                }
            }
        }
        stage('UNIT testing'){
            
            steps{
                
                script{
                    
                    sh 'mvn test'
                }
            }
        }
        stage('Integration testing'){
            
            steps{
                
                script{
                    
                    sh 'mvn verify -DskipUnitTests'
                }
            }
        }
        stage('Maven build'){
            
            steps{
                
                script{
                    
                    sh 'mvn clean install'
                }
            }
        } 
        stage('Sonar Analysis'){
            environment{
                     scannerHome = tool 'sonar4.8'
            }

         steps {
            withSonarQubeEnv('sonar-token1') {
               sh '''${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=nexus_helm_cicd_app \
                   -Dsonar.projectName=nexus_helm_cicd_app \
                   -Dsonar.projectVersion=1.0 \
                   -Dsonar.sources=src/ \
                   -Dsonar.java.binaries=target/test-classes/com/visualpathit/account/controllerTest/ \
                   -Dsonar.junit.reportsPath=target/surefire-reports/ \
                   -Dsonar.jacoco.reportsPath=target/jacoco.exec \
                   -Dsonar.java.checkstyle.reportPaths=target/checkstyle-result.xml'''
            }
         }

        }
    }

}         