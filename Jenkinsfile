pipeline{
    
    agent any
    tools {
        jdk 'JAVA_HOME'
        maven 'MAVEN_HOME'
    }
    environment {
        PATH = "$PATH:C:/maven/apache-maven-3.9.6-bin (3)/apache-maven-3.9.6/bin"
    }
    stages{
       // stage('code source'){
       //      steps{
       //          git branch: 'master', changelog: false, poll: false, url: 'https://github.com/PanchalOm/mybatis-3.git'
       //      }
       //   } 
         
       stage('Code Compile'){
            steps{
                 bat 'mvn clean compile'
                
            }
         }
         
         
       stage('Unit test'){
            steps{
                 bat 'mvn test'
                
            }
         }
         
        stage('Integration test'){
            steps{
                 bat 'mvn verify -DskipUnitTests'
                
            }
         }
         
         stage('Maven build'){
            steps{
                 bat 'mvn clean install'
                
            }
         }
        
         stage('OWASP Dependency Check'){
            steps{
                 dependencyCheck additionalArguments: '', odcInstallation: 'DP'
                
            }
         } 
         
       stage('Testing by sonar'){
            steps{
                
                 bat ''' mvn sonar:sonar -Dsonar.url-http://localhost:9000/ -Dsonar.login-squ_abb67d36969df874cb80b76166032e71de78defa -Dsonar.projectname-mybatis \
                     -Dsonar.java.binaries=. \
                     -Dsonar.projectKey=mybatis '''
            
            }
         }   
         
        stage('Code build'){
            steps{
                
                 bat 'mvn clean package'
            
            }
         } 
         
//         stage('Email notification'){
//             steps{
//                mail bcc: '', body: '''Your Mybatis pipeline is successfully compeleted.

// For check your job connect with jenkins. 

// Thanks
// -Devops Team Ximple Solutions''', cc: '', from: '', replyTo: '', subject: 'migrations result', to: 'ompanchalait@gmail.com'
                
//             }
//          }
    }
    post{
        
          success{
            
             emailext attachLog: true, body: '''Your Mybatis pipeline is successfully completed.<br>
For check pipeline result is click the blog.<br><br>

Thanks.<br>
-DevOps Team Ximple Solutions''', subject: 'Mybatis pipeline result', to: 'ompanchalait@gmail.com'
           
            }
        failure{
            emailext attachLog: true, body: '''Your Mybatis pipeline is unfortunately failed.<br>
For check pipeline result is click the blog.<br><br>

Thanks.<br>
-DevOps Team Ximple Solutions''', subject: 'Mybatis pipeline result', to: 'ompanchalait@gmail.com'
           
        }
    }
}
