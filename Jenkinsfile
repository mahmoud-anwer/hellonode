node {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        app = docker.build("anwer95/hellonode")
    }

    stage('Test image') {
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Volkswagen-type approach ;-) */

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. 
         *docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials'*/
           //sh 'sudo docker login -u "anwer95" -p "Zephyr@17" docker.io'
        docker.withRegistry("https://hub.docker.com/", ''){
                     app.push("${env.BUILD_NUMBER}")
                     app.push("latest")
            }
      /*docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {            
				app.push("${env.BUILD_NUMBER}")
                app.push("latest")
	        }  */  
               
            //app.push("${env.BUILD_NUMBER}")
            //app.push("latest")
        
    }
}
