
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
                        rpm -ivh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
                        subscription-manager repos --enable "rhel-*-optional-rpms" --enable "rhel-*-extras-rpms"
                        yum update
                        yum install snapd
                        systemctl enable --now snapd.socket
                        ln -s /var/lib/snapd/snap /snap
                        snap install helm --classic
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

