node {
    def app

    stage('Clone repository') {
        /* Cloning the Repository to our Workspace */

       git credentialsId: 'git_hub', 
       url: 'https://github.com/curiouslove/NodeApp.git'

    }

    stage('Build image') {
	    
       sh('docker build -t lovie1234/nodeapp:3.0 .')
    }

    stage('Login into Docker Hub') {

        withCredentials([string(credentialsId: 'docker_hub_pwd', variable: 'docker-pwd')]) {
        }
	    
        sh('docker login -u lovie1234 -p ${docker-pwd}')
    }

    stage('Push image') {
        /* 
			You would need to first register with DockerHub before you can push images to your account
		*/
//         docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
//             app.push("${env.BUILD_NUMBER}")
//             app.push("latest")
//             } 
//                 echo "Trying to Push Docker Build to DockerHub"
	    sh('docker push lovie1234/nodeapp:3.0')
    }
	
    stage('Deploy Node-app Container ') {
	    
        sh('docker run -d -p 8000:8000 lovie1234/nodeapp:3.0')
    }

}
