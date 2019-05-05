node ('master') {
  stage('Clone repository') {
    /* Let's make sure we have the repository cloned to our workspace */
    checkout scm
  }
  stage('Build') {
    dockerImage = docker.build("nginx-test")
  }
  stage('Run') {
    sh "docker container rm -f nginx-test"
    sh "docker run --name nginx-test -p 8081:80 -d nginx-test"
    //docker.image('nginx-test').withRun('--name nginx-test -p 8081:80 -d') {
            /* do things */
    //    }
  }
  stage('Test image') {
    /* Ideally, we would run a test framework against our image.
     * For this example, we're using a Volkswagen-type approach ;-) */

    //dockerImage.inside {
    //sh 'echo "Tests passed"'
    }
  }

  stage('Push image') {
    /* Finally, we'll push the image with two tags:
     * First, the incremental build number from Jenkins
     * Second, the 'latest' tag.
     * Pushing multiple tags is cheap, as all the layers are reused. */
     docker.withRegistry('', 'crash430') {
     dockerImage.push("latest")
     }
  }
}
