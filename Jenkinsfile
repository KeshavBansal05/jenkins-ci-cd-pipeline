pipeline {
    agent any
    //environment variables
    environment{
        DIRECTORY_PATH="/directory_path_code_directory"
        TESTING_ENVIRONMENT = "Test Env"
        PRODUCTION_ENVIRONMENT = "Prod Env"
    }

    //stages for the pipeline
    stages{
         stage('Build') {  //for creating the build
             
             steps{
                 echo "fetch the source code from the directory path specified by the environment variable"
                 echo "compile the code and generate any necessary artifacts"
             }
       
    }
    
     stage('Unit and Integration Tests') { // for running tests
             steps{
            
                 echo "unit tests"
                 echo "integration tests"
                
            
              
                    emailext (
                subject: "Jenkins Build ${env.BUILD_NUMBER} - Test Stage ${currentBuild.result}",
                body: "The Test stage of build ${env.BUILD_NUMBER} has completed with status: SUCCESS.",
                to: 'keshav4788.be23@chitkara.edu.in',
                attachLog: true
            )
                
             }
    }
             
       
    
    
    
     stage('Code Analysis') { //for checking the quality of the code
             
             steps{
                 echo "check the quality of the code"
                 echo "Using sonarqube for checking code quality"
             }
       
    }

     stage('Security scan') { //for checking the quality of the code
             
            steps{
       
            
             
                 echo "Security scan using OWASP Dependency-Check plugin for checking project dependencies for vulnerabilities"
            
                    emailext (
                subject: "Jenkins Build ${env.BUILD_NUMBER} - Security Scan Stage ${currentBuild.result}",
                body: "The Security Scan stage of build ${env.BUILD_NUMBER} has completed with status: SUCCESS.",
                to: 'keshav4788.be23@chitkara.edu.in',
                attachLog: true
            )
                
             }
       
     }
    
     stage('Deploy') { //Deployment into staging environment
             
             steps{
                 echo "deploy the application to a testing/staging environment in an AWS EC2 instance"
                 echo "test environment: ${TESTING_ENVIRONMENT}"
             }
       
    }
        
    
    
      stage('Integration Tests on Staging') {  //Build approval stage for production deployment
             
             steps{
                
                echo "Running integration tests on staging environment"
                echo "Tests complete"
             }
       
    }

    stage('Deploy to production') { //production deployment
             
             steps{
                 echo "Deploying to production environment: ${PRODUCTION_ENVIRONMENT}"
                 echo "Deployed to production!"
             }
       
    }

    
    }

    post{
        always{
        emailext (
      subject: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
      body: """<p>SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
        <p>Check console output at &QUOT;<a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>""",
      to: "keshav4788.be23@chitkara.edu.in"
    )
    }
    }

} 
