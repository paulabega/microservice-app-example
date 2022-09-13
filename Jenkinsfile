pipeline {
    agent any 
    stages {
        stage('Clone Jenkins repository') { 
          steps {
            checkout(scm)
            }
        }

        stage('Build and push users-api') { 
            steps {
                dir("users-api"){
                    script {
                        def UsersAPI = docker.build('paulabetancurg/users-api')
                        docker.withRegistry('https://registry.hub.docker.com', 'DockerHubCredential') {
                            UsersAPI.push('latest')
                        }
                    }

                }

            }
        }

    }
}
