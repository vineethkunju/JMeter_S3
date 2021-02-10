pipeline{
 
  agent any
  
  stages{
  	
  	stage('Execute Test'){
    
	    steps{
	 	 
			sh '''#!/bin/bash
			cd /home/ec2-user/apache-jmeter-5.4/bin
			echo "Starting execution"
			sudo sh jmeter.sh -n -t  /home/ec2-user/JMeterContents/Scripts/DemoScript-DummySampler_V0.1.jmx -l /home/ec2-user/JMeterContents/Results/DemoScript-DummySampler.csv -e -o  /home/ec2-user/JMeterContents/HTMLReport/'''
	      }  	    
	  
	  	}

	stage('Upload S3'){
	    
	    steps{
	    	 sh '''#!/bin/bash
			CURRENTEPOCTIME=`date +"%s"`
			cd /home/ec2-user/JMeterContents/HTMLReport/
			aws s3api put-object --bucket bat.jmeterresults --key ${CURRENTEPOCTIME}/
			aws s3 sync . s3://bat.jmeterresults/${CURRENTEPOCTIME}/'''
	      }  	    
	  	}
  	
  	
  	stage('Clean Workspace'){
    
    steps{
    	 sh '''#!/bin/bash
		sudo rm -r /home/ec2-user/JMeterContents/HTMLReport/*.*
		sudo rm -r /home/ec2-user/JMeterContents/HTMLReport/content
		sudo rm -r /home/ec2-user/JMeterContents/Results/*.*
		'''
      }  	    
  	}
  	
  	stage('Send Mail'){
  	    
  	    steps{
  	        emailext body: '''You can find your results from
			http://bat.jmeterresults.s3-website.eu-west-2.amazonaws.com/${CURRENTEPOCTIME}/index.html''', subject: 'Performance Test Results', to: 'vineethpk@gmail.com'
  	    }
	}

   }

}
