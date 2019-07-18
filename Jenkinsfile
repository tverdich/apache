pipeline {
    agent any
    stages {
        stage('Delete the workspace') {
            steps {
                sh "sudo rm -rf $WORKSPACE/*"
            }
        }
        stage('Installing ChefDK') {
            steps {
                script {
                    def exists = fileExits '/usr/bin/chef-client'
                    if (exists) {
                        echo "Skipping CheDk install - allready installed"
                    } else {
                        sh 'export CHEF_LICENSE=accepted'
                        sh 'sudo apt-get install wget -y'
                        sh 'wget https://packages.chef.io/files/stable/chefdk/3.8.14/ubuntu/18.04/chefdk_3.8.14-1_amd64.deb'
                        sh 'sudo dpkg -i chefdk_3.8.14-1_amd64.deb'  
                    }
                }
            }
        }
        stage('Download Apache Cookbook') {
            steps {
                git credentialsId: 'git-repo-creds', url: 'git@github.com:tverdich/apache.git'
            }
        }
    }
}