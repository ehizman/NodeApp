node {
    def app

    stage('Clone repository') {
        git credentialsId: '21effd52-5e41-4f06-9b91-6c28482be12e', 
        url: 'https://github.com/ehizman/NodeApp'
    }

    stage('Build image') {
        withCredentials([string(credentialsId: 'Docker_Hub_Pwd', variable: 'Docker-Pwd')]) {
        }
       sh('docker build -t ehizman/node-app:2.0 .')
    }

    stage('Login into Docker Hub') {
        
        sh("docker login -u ehizman -p ${Docker-Pwd}")
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
        sh('docker push ehizman/node-app:2.0')
    }
    
    stage('Deploy Node-App Container ') {
        
        sh('docker run -d -p 8000:8000 ehizman/node-app:2.0')
    }

}
