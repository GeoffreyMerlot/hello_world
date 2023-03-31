pipeline {
    //agent any
    agent { label 'etiquetteLinux' }
    
    stages {
        stage('BEGIN') {
            steps {
                //sh 'echo Hey !'
                echo 'Begin pipeline !'
            }
        }
        
        stage('Checkout') {
            steps {
               git branch: 'main', credentialsId: 'bde2a104-5470-41d8-9257-c84f7c4f8ea3', url: 'git@github.com:GeoffreyMerlot/hello_world.git' 
            }
        }
        
        stage('Compile') {
            steps {
                sh 'mvn generate-test-resources process-test-resources'
                sh 'mvn compile'
            }
        }
        
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        
        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }
        
        stage('action SH') {
            steps {
                sh label: 'Liste répertoire courant', script: '''pwd; ls -lrtR'''
            }
        }
        
        stage('END') {
            steps {
                echo 'Close pipeline'
            }
        }
    }
    
    post {
        always {
            echo 'PIPELINE ALWAYS'
        }
        success {
            //echo 'PIPELINE SUCCESS'
            archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
        }
        failure {
            mail bcc: '', body: '<b>Example</b><br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL de build: ${env.BUILD_URL}', cc: '', from: '', replyTo: '', mimeType: 'text/html', subject: 'Error My_Pipeline', to: 'merlot.geoffrey@gmail.com'
        }
        unstable {  
             echo 'This will run only if the run was marked as unstable'  
         }  
         changed {  
             echo 'This will run only if the state of the Pipeline has changed'  
             echo 'For example, if the Pipeline was previously failing but is now successful'  
         }
    }
}
