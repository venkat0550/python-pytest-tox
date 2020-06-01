node ('dockerslave1') {
    
    stage('Check out SCM'){
	    	git 'https://github.com/venkat0550/python-roche.git'
	    	sh("docker images")

	}
   	stage('Build Image and Run commands on Container'){
		def python = docker.build("python:38")
		python.inside('-v ${WORKSPACE}:/opt'){
        sh """
        cd multipython/ && ls && pwd
        cat tox.ini
        sed -i 's/^envlist =.*/envlist = py38/' tox.ini
        cat tox.ini
        tox
        """
       // sh("cat squarer.py")
        }	
  	    
   	}
   	stage('Remove the image from Node'){
	    sh ("docker rmi python:38")
		sh """
		docker images
		"""
	}
    stage('Workspace Cleanup'){
        cleanWs()  
    }
}

