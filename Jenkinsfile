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

        stage('Build and push todos-api') { 
            steps {
                dir("todos-api"){
                    script {
                        def todosAPI = docker.build('paulabetancurg/todos-api')
                        docker.withRegistry('https://registry.hub.docker.com', 'DockerHubCredential') {
                            todosAPI.push('latest')
                        }
                    }

                }

            }
        }

        stage('Build and push log-message-processor') { 
            steps {
                dir("log-message-processor"){
                    script {
                        def logMessageProcessor = docker.build('paulabetancurg/log-message-processor')
                        docker.withRegistry('https://registry.hub.docker.com', 'DockerHubCredential') {
                            logMessageProcessor.push('latest')
                        }
                    }

                }

            }
        }

        stage('Deploy') {
            steps {
                sshagent(['SSHKey']) {
                    sh 'ssh ubuntu@10.1.1.33 ansible-playbook docker.yaml -i inventory.yaml -v'
                }
            }
        }

    }
}
