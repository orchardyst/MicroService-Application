pipeline {
    agent any
    environment {
        SCANNER_HOME = tool 'sonar-scanner'

   }

    stages {
            stage('SonarQube') {
             steps {
                withSonarQubeEnv('sonar') {
                    sh '''$SCANNER_HOME/bin/sonar-scanner -Dsonar.projectKey=Microservice_Deployment -Dsonar.ProjectName=Microservice_Deployment -Dsonar.java.binaries=.'''
                }
            }
        } 
  
      
      stage('adservice') {
              steps {
               script {
                 withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                    dir('/var/lib/jenkins/workspace/Microservice_Deployment/src/adservice/') {
                        sh "docker build -t orchardyst/adservice:latest ."
                        sh "docker push orchardyst/adservice:latest"
                        sh "docker rmi orchardyst/adservice:latest"
                    }
                }
            }
        }
            }
            stage('cartservice') {
              steps {
               script {
                 withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                    dir("/var/lib/jenkins/workspace/Microservice_Deployment/src/cartservice/src/") {
                        sh "docker build -t orchardyst/cartservice:latest ."
                        sh "docker push orchardyst/cartservice:latest"
                        sh "docker rmi orchardyst/cartservice:latest"
                    }
                }
            }
        }
       }
stages {
        stage('Cleanup Docker Environment') {
            steps {
                script {
                    sh 'docker system prune -af'
                }
            }
        }
}
    stage('Cleanup Go Modules Cache') {
    steps {
        script {
            sh 'docker run --rm -v $(pwd):/app -w /app golang go clean -cache -modcache'
        }
    }
}
            stage('checkoutservice') {
              steps {
               script {
                 withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                    dir("/var/lib/jenkins/workspace/Microservice_Deployment/src/checkoutservice/") {
                        sh "docker build -t orchardyst/checkoutservice:latest ."
                        sh "docker push orchardyst/checkoutservice:latest"
                        sh "docker rmi orchardyst/checkoutservice:latest"
                    }
                }
            }
        }
            }
            stage('currencyservice') {
              steps {
               script {
                 withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                    dir("/var/lib/jenkins/workspace/Microservice_Deployment/src/currencyservice/") {
                        sh "docker build -t orchardyst/currencyservice:latest ."
                        sh "docker push orchardyst/currencyservice:latest"
                        sh "docker rmi orchardyst/currencyservice:latest"
                    }
                }
            }
        }

            }
            stage('emailservice') {
              steps {
               script {
                 withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                    dir("/var/lib/jenkins/workspace/Microservice_Deployment/src/emailservice/") {
                        sh "docker build -t orchardyst/emailservice:latest ."
                        sh "docker push orchardyst/emailservice:latest"
                        sh "docker rmi orchardyst/emailservice:latest"
                    }
                }
            }
        }
            }
            stage('frontend') {
              steps {
               script {
                 withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                    dir("/var/lib/jenkins/workspace/Microservice_Deployment/src/frontend/") {
                        sh "docker build -t orchardyst/frontend:latest ."
                        sh "docker push orchardyst/frontend:latest"
                        sh "docker rmi orchardyst/frontend:latest"
                    }
                }
            }
        }
            }
            stage('loadgenerator') {
              steps {
               script {
                 withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                    dir("/var/lib/jenkins/workspace/Microservice_Deployment/src/loadgenerator/") {
                        sh "docker build -t orchardyst/loadgenerator:latest ."
                        sh "docker push orchardyst/loadgenerator:latest"
                        sh "docker rmi orchardyst/loadgenerator:latest"
                    }
                }
            }
        }
            }
             stage('paymentservice') {
              steps {
               script {
                 withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                    dir("/var/lib/jenkins/workspace/Microservice_Deployment/src/paymentservice/") {
                        sh "docker build -t orchardyst/paymentservice:latest ."
                        sh "docker push orchardyst/paymentservice:latest"
                        sh "docker rmi orchardyst/paymentservice:latest"
                    }
                }
            }
        }
             }
             stage('productcatalogservice') {
              steps {
               script {
                 withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                    dir("/var/lib/jenkins/workspace/Microservice_Deployment/src/productcatalogservice/") {
                        sh "docker build -t orchardyst/productcatalogservice:latest ."
                        sh "docker push orchardyst/productcatalogservice:latest"
                        sh "docker rmi orchardyst/productcatalogservice:latest"
                    }
                }
            }
        }
             }
             stage('recommendationservice') {
              steps {
               script {
                 withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                    dir("/var/lib/jenkins/workspace/Microservice_Deployment/src/recommendationservice/") {
                        sh "docker build -t orchardyst/recommendationservice:latest ."
                        sh "docker push orchardyst/recommendationservice:latest"
                        sh "docker rmi orchardyst/recommendationservice:latest"
                    }
                }
            }
        }
             }
             stage('shippingservice') {
              steps {
               script {
                 withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                    dir("/var/lib/jenkins/workspace/Microservice_Deployment/src/shippingservice/") {
                        sh "docker build -t orchardyst/shippingservice:latest ."
                        sh "docker push orchardyst/shippingservice:latest"
                        sh "docker rmi orchardyst/shippingservice:latest"
                    }
                }
            }
        }
    }

              stage('EKS-Deployment') {
            steps {
                withKubeConfig(caCertificate: '', clusterName: 'myAppp-eks-cluster', contextName: '', credentialsId: 'K8s', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://E4F6F23FCD3EB5AF04D37C33B1043064.gr7.us-east-1.eks.amazonaws.com') {
                    sh 'kubectl apply -f deployment-service.yaml'
                    sh 'kubectl get pods'
                    sh 'kubectl get svc'

                }
                }
            }
        }
   }
