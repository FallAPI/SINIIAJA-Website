pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "SINIIAJA/SINIIAJA:latest"
        DOCKER_CONTAINER = "SINIIAJA"
        PORT_MAPPING = "8089:80"
    }

    stages{
        stage("clone repository"){
            steps{
                deleteDir()
                checkout([$class: gitSCM, branches:[name: "master"], userRemoteConfigs: [url: "https://github.com/FallAPI/SINIIAJA-Website.git"]])
            }
        }
        stage("build Docker Image"){
            steps{
                script{
                    docker.build(env.DOCKER_IMAGE)
                }
            }
        }
        stage("Run Docker Container"){
            steps{
                script{
                    docker.image(env.DOCKER_IMAGE).run("-d --name ${env.DOCKER_CONTAINER} -p ${env.PORT_MAPPING}")
                }
            }
        }
    }
}