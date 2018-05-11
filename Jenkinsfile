node {
    docker.withRegistry('https://hub.docker.com/', 'docker-hub-credentials') {
    	def mvnHome
    	
    	stage('checkout'){
        
        mvnHome = tool 'M3'
        git url: 'https://github.com/prakashg1984/workplace.git'
    
        sh "git rev-parse HEAD > .git/commit-id"
        def commit_id = readFile('.git/commit-id').trim()
        println commit_id
        }
    
    dir('testnewproject'){
        stage('build'){
	        sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean install"
    	}
    	
    	stage('create docker image'){
		        sh 'docker login --username prakashg84 --password kashprag0712'
		        sh ("docker build -t testnewproject .")
		        sh ("docker tag  testnewproject prakashg84/test:testnewproject")
    	}
    	
    	stage('push docker image'){
			sh ("docker push prakashg84/test:testnewproject")
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
    }
}
