node {
	stage ('checkout') {
		sh "git clone https://github.com/dhineshk6/kubdemo.git"
	}
        stage('build'){
	        sh "mvn -f /var/lib/jenkins/workspace/kubedemo/kubdemo clean install"
    	}
    	
    	stage('create docker image'){
		        
		        sh ("docker build -t testnewproject .")
		        sh ("docker tag  testnewproject dhineshk6/test:testnewproject")
    	}
    	
    	stage('push docker image'){
			sh ("docker push dhineshk6/test:testnewproject")
    	}
    	
    	stage('create deployment'){
    	    sh 'kubectl delete deployments testnewprojectapi || true' 
	    sh 'kubectl create -f deployment.yaml --validate=false'
    	}
    	
    	stage('create service'){
	    sh 'kubectl delete services testnewprojectapiservice || true'
	    sh 'kubectl create -f services.yaml --validate=false'
    	}
    }
