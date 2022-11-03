
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
                        helm upgrade -i apache myapache --namespace jenkins-test --debug
                    '''
                }
        sleep 60
            }
        }
    }

}


pipeline {
    agent any;
    stages {
        stage('debug') {
            steps {
                withCredentials([
                    file(credentialsId: 'kubeconfig', variable: 'FILE'),
                    [
                        $class: 'AmazonWebServicesCredentialsBinding',
                        accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                        credentialsId: 'awstoEKS',
                        secretKeyVariable: 'AWS_SECRET_ACCESS_KEY'
                    ]
                    
                ]) {
                    
                  
                  sh """
                    cat $FILE
                    curl -u $AWS_ACCESS_KEY_ID:$AWS_SECRET_ACCESS_KEY https:/do.something.aws.com > output
                  """
                }
            }
        }
    }
}
