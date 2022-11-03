
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

   stages('Kubernets deploy') {
        steps {
   withCredentials([
       file(credentialsId: 'kubeconfig', variable: 'kubeconfig'), {
                script {
                    sh '''
                        helm upgrade -i apache myapache --namespace jenkins-test --debug
                    '''
                }
        sleep 60
            }
        }
    }

}
