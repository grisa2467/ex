
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
#            withCredentials([kubeconfigFile(credentialsId: "EKS-${ENVIRONMENT}", variable: 'KUBECONFIG'), string(credentialsId: "${ENVIRONMENT}_bonus-management-db_pass_base64", variable: 'IBETUSER_DB_PASSWORD'), usernamePassword(credentialsId: 'jenkins-ibet', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                script {
                    sh '''
                                helm upgrade -i apache myapache --namespace jenkins-test --debug
                        fi
                    '''
                }
        sleep 60
            }
        }
    }

}