pipeline {
    agent none
    stages {
        stage('Image creation & image push') {
            agent any
            steps {
                
		        
                echo "Pulling dependecies"
                sh "docker pull -f ditas/vdc-base-image"
                echo "BUILDING THE IMAGE"
                sh "docker build -t \"ditas/nodejs-base-image\" -f Dockerfile ."
                echo "Done"
		    
                echo 'Retrieving Docker Hub password from /opt/ditas-docker-hub.passwd...'
                script {
                    password = readFile '/opt/ditas-docker-hub.passwd'
                }
                echo "Done"

                echo 'Login to Docker Hub as ditasgeneric...'
                sh "docker login -u ditasgeneric -p ${password}"
                echo "Done"

                echo "Pushing the image ditas/nodejs-base-image:latest..."
		        sh "docker push ditas/nodejs-base-image"
                echo "Done "
            }
        }
    }
}
