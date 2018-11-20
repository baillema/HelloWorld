pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Hello world!' 
                echo 'Coucou !' 
                echo 'Welcome !'
                script {    
                  docker.withTool('latest') {
                    docker.image('maven:3-jdk-8-slim').inside("-v $WORKSPACE:/usr/src/myproject:rw -v $HOME/.m2:/root/.m2:rw -w /usr/src/myproject") { c ->
                      sh "mvn clean package"
                    }
                  }
                }
            }
        }
        stage('Package app') {
            steps {
                script {    
                  docker.withTool('latest') {
                    docker.withRegistry('https://registry.uggla.fr/') {
                      def myImg = docker.build("my-image:${env.BUILD_ID}")
                    }
                  }
                }
            }
        }
    }
}
