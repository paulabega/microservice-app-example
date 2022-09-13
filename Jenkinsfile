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
                        def usersAPI = docker.build('paulabetancurg/users-api')
                        docker.withRegistry('https://registry.hub.docker.com', 'DockerHubCredential') {
                            usersAPI.push('latest')
                        }
                    }

                }

            }
        }

        stage('Build and push auth-api') { 
            steps {
                dir("auth-api"){
                    script {
                        def authAPI = docker.build('paulabetancurg/auth-api')
                        docker.withRegistry('https://registry.hub.docker.com', 'DockerHubCredential') {
                            authAPI.push('latest')
                        }
                    }

                }

            }
        }

    }
}
