@Library('libx@main')_

pipeline{
    agent {
        label 'bash'
    }

    tools{
        jdk "java-8"
    }

    environment{
        DOCKER_USER = credentials('dockerhub-user')
        DOCKER_PASS = credentials('dockerhub-password')
    }

    // parameters {
    //     string defaultValue: '${BUILD_NUMBER}', description: 'Enter the version of the docker image', name: 'VERSION'
    // }

    stages{
        stage("build java app image"){
            steps{
                script{
                    def dockerx = new org.iti.docker()
                    dockerx.build("java", "${BUILD_NUMBER}")
                }
                sh "docker login -u ${DOCKER_USER} -p ${DOCKER_PASS} "
            }
        }
        stage("push java app image"){
            steps{
                script{
                    def dockerx = new org.iti.docker()
                    dockerx.login("${DOCKER_USER}", "${DOCKER_PASS}")
                    dockerx.push("${DOCKER_USER}", "${DOCKER_PASS}")
                }
            }
        }
    }
}