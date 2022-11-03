
final boolean Deploy = env.DEPLOY == "true"

pipeline {
   agent any
   environment {
        npm_config_cache ='/opt/bitnami/jenkins/jenkins_home/wokspace'
   }
   tools {
     maven 'maven_3_6_3'
     jdk 'jdk11'
   }

   stages {
       stage('Kubernets deploy') {
        steps {
           withCredentials([
               file(credentialsId: 'kubeconfig', variable: 'kubeconfig')]) {
                script {
                    sh '''
                        yum update
                        curl -L https://mirror.openshift.com/pub/openshift-v4/clients/helm/latest/helm-linux-amd64 -o /usr/local/bin/helm
                        chmod +x /usr/local/bin/helm
                        helm version
                        sleep 60
                        helm upgrade -i apache myapache --namespace jenkins-test --debug
                    '''
                }
        sleep 60
            }
        }
    }
   }
}

