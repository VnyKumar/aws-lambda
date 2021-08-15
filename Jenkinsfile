pipeline {
    agent {
        label '!windows'
    }

    environment {
       	FUNC_NAME   = 'demo-function'
	TEST_FUNC   =  'temp'
	  
    }
     triggers {
        pollSCM "* * * * *"
    }
	
	
    stages {
        stage('clone') {
            steps {
                
		 sh 'mvn -B -DskipTests clean package'
		 sh 'pwd'
		                 
            }//steps
        }//stage
	    
	    stage('upload to s3'){
		    steps {
		    sh 'echo in s3 upload..'
		    //sh 'aws s3 ls'
		   
		   /* withAWS(credentials:'AWS-S3-Lambda') {
				sh "aws s3 ls s3://aws22bucket/ --recursive"
			        //sh "aws s3 cp ../*.jar  s3://aws22bucket --recursive"
			        sh 'aws lambda update-function-code  --function-name  demofunction3   --zip-file fileb://target/lambda-java-api-example-1.0-SNAPSHOT.jar'
                                    
			    }*/
	/// Prasadu changes
			    
			    withAWS(region:'us-west-2',credentials:'AWSLoginCred'){
				   sh 'aws lambda list-functions'
				   sh "aws lambda create-function --function-name demo-function --zip-file fileb://target/lambda-java-api-example-1.0-SNAPSHOT.jar --handler com.techprimers.aws.LambdaJavaAPI --runtime java8 --role arn:aws:iam::125855726099:role/lambda-example"
				   // sh 'echo "${FUNC_NAME}'
				    //sh 'aws function-exists --function-name "temp" '
				    

				    sh 'aws lambda list-functions | grep -i ${TEST_FUNC} ' 
				  
			    
			    }
			    
		    }
	    }
        
    }//stages
	
}//pipeline
