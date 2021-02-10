pipeline{
 
  agent any
  
  stages{
  	
  	stage('JMX Download'){
    
	    steps{
	    	 echo 'found something interesting'
	    	 
	    	 git branch: 'JMX', credentialsId: '3f527557-74c4-4e20-8d9a-c50b52c76a23', url: 'https://github.com/vineethkunju/WTC_JP.git'
	      }  	    
	  
	  	}

	stage('Deploy'){
	    
	    steps{
	    	 echo 'found something interesting'
	      }  	    
	  	}
  	
  	stage('Test'){
    
    steps{
    	 echo 'found something interesting'
      }  	    
  	}

  
  }

}
