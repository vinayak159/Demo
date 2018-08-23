pipeline {
         agent any
         stages {
                 stage('SonarQube Analysis') {
                 steps {
                    input('Do you want to proceed?')
                    withSonarQubeEnv('sonar') {
                    //requires SonarQube Scanner for Maven 3.2+
                    bat 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.2:sonar'
                        }
                     }         
                  }
                  stage("SonarQube Quality Gate") { 
                  steps {
                    input('Do you want to proceed?')       
                    timeout(time: 1, unit: 'MINUTES') { 
                    waitForQualityGate abortPipeline: true
                     }        
                   }
                 }
                 stage('Code Build') {
                 steps     {
                           input('Do you want to proceed with build & war creation?')
                           withMaven(
                           // Maven installation declared in the Jenkins "Global Tool Configuration"
                           maven: 'mvn',
                           // Maven settings.xml file defined with the Jenkins Config File Provider Plugin
                           // Maven settings and global settings can also be defined in Jenkins Global Tools Configuration
                           mavenSettingsConfig: 'maven',
                           mavenLocalRepo: 'C:\\Users\\330406\\.m2\\repository') {
                           // Run the maven build
                           bat 'mvn clean package'

                           }   
                           echo "war creation successful!!"
                       }
                 }
                 stage('Dev Deployment') {
                 steps {
                        input('Do you want to proceed with Dev deployment?')
                        bat 'D:\\Essentials\\WAS855\\AppServer85\\profiles\\AppSrv01\\bin\\wsadmin -lang jython -f D:\\Vinayak\\Learning\\WAS_Deploy_Script\\installApplication.py'
                        echo "Dev Deployment Successful!!"
                       }
                 }
                 stage('Testing') {
                 steps {
                         input('Do you want to proceed with Testing?') 
                         echo "Testing Successful!!"
                           }
                 }
                 stage('Prod Deployment') {
                 steps {
                         input('Do you want to proceed with Production deployment?')
                         echo "Production Deployment Successful!!"
                           }
                 }
         }
}
