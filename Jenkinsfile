pipeline {
    agent {
        kubernetes {
            yamlFile "kaneki.yaml"
        }
    }

    stages {
        stage("Pulling git repo and building the image") {
            steps{
                container("kaniko") {
                    git url: "https://github.com/JIN4HOCTb/DevOps-2-docker-.git", branch: "main"
                    sh "/kaniko/executor --context . --destination h0neyball/test:${env.BUILD_NUMBER}"
                }
            }
        }

        stage("Pull image and run.") {
            agent {
                kubernetes {
                    yaml """
                    apiVersion: v1
                    kind: Pod
                    metadata:
                      name: "honeyball_image"
                    spec:
                      containters:
                        - name: "hb_image"
                          image: h0neyball/test:${env.BUILD_NUMBER}
                    """
                }
            }
            steps {
                sh "sleep 99d"
            }
        }
    }
}
