pipeline {
    agent any

    stages {

        stage('Checkout AnsibleLab') {
            steps {
                dir('AnsibleLab') {
                    git branch: 'main',
                        url: 'https://github.com/hack3rinsider/AnsibleLab.git'
                }
            }
        }

        stage('Checkout Banking-App') {
            steps {
                dir('Banking-App') {
                    git branch: 'main',
                        url: 'https://github.com/hack3rinsider/Banking-App.git'
                }
            }
        }

        stage('Cleanup Old Lab') {
            steps {
                sh '''
                docker rm -f controller web1 web2 web3 db1 mon1 || true
                docker network rm ansiblelab_ansible-net || true
                '''
            }
        }

        stage('Build Lab Infrastructure') {
            steps {
                sh '''
                cd AnsibleLab
                docker compose up -d --build
                '''
            }
        }

        stage('Verify Lab Infrastructure') {
            steps {
                sh '''
                docker ps --format "table {{.Names}}\t{{.Status}}"
                '''
            }
        }

        stage('Deploy Banking App') {
            steps {
                sh '''
                docker cp Banking-App/ansible/deploy-banking.yml controller:/ansible/
                docker cp Banking-App/ansible/inventory.ini controller:/ansible/

                docker exec controller \
                ansible-playbook \
                -i /ansible/inventory.ini \
                /ansible/deploy-banking.yml
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                sh '''
                docker exec controller \
                ansible web \
                -i /ansible/inventory.ini \
                -m ping
                '''
            }
        }

        stage('Application Health Check') {
    steps {
        sh '''
        docker exec web1 curl -f http://localhost
        '''
    }
}
    }

    post {
        success {
            echo 'Banking App deployed successfully'
        }

        failure {
            echo 'Deployment failed'
        }
    }
}
