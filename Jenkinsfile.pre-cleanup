pipeline {


agent any

parameters {

    choice(
        name: 'TARGET_ENV',
        choices: ['BLUE', 'GREEN'],
        description: 'Environment to deploy'
    )

}

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

    stage('Build Infrastructure If Missing') {

        steps {

            sh '''
            if ! docker ps -a --format "{{.Names}}" | grep -q "^controller$"; then

                echo "Building Infrastructure..."

                cd AnsibleLab
                docker compose up -d --build

            else

                echo "Infrastructure already exists"

            fi
            '''

        }

    }

    stage('Verify Infrastructure') {

        steps {

            sh '''
            docker exec controller \
            ansible all \
            -i /ansible/inventory.ini \
            -m ping
            '''

        }

    }

    stage('Current Production Environment') {

        steps {

            sh '''
            echo "===== CURRENT PRODUCTION ====="

            docker exec controller \
            ansible lb \
            -i /ansible/inventory.ini \
            -m shell \
            -a "curl -s http://localhost/api/"
            '''

        }

    }

    stage('Copy Ansible Files') {

        steps {

            sh '''
            docker cp Banking-App/ansible/inventory.ini controller:/ansible/
            docker cp Banking-App/ansible/deploy-bluegreen.yml controller:/ansible/
            docker cp Banking-App/ansible/switch-traffic.yml controller:/ansible/
            '''

        }

    }

    stage('Deploy Selected Environment') {

        steps {

            script {

                def deployGroup =
                    params.TARGET_ENV == 'BLUE'
                    ? 'blue'
                    : 'green'

                sh """
                docker exec controller \
                ansible-playbook \
                -i /ansible/inventory.ini \
                -e target_env=${deployGroup} \
                /ansible/deploy-bluegreen.yml
                """

            }

        }

    }

    stage('Health Check Target Environment') {

        steps {

            script {

                if (params.TARGET_ENV == 'BLUE') {

                    sh '''
                    docker exec controller \
                    ansible blue \
                    -i /ansible/inventory.ini \
                    -m shell \
                    -a "curl -s http://localhost:3000"
                    '''

                } else {

                    sh '''
                    docker exec controller \
                    ansible green \
                    -i /ansible/inventory.ini \
                    -m shell \
                    -a "curl -s http://localhost:3000"
                    '''

                }

            }

        }

    }

    stage('Deployment Summary') {

        steps {

            echo "Target Deployment Environment: ${params.TARGET_ENV}"

        }

    }

    stage('Manual Approval') {

        steps {

            input message: "Switch production traffic to ${params.TARGET_ENV} ?"

        }

    }

    stage('Blue Green Traffic Switch') {

        steps {

            script {

                def backendTarget =
                    params.TARGET_ENV == 'BLUE'
                    ? 'web1'
                    : 'web2'

                sh """
                docker exec controller \
                ansible-playbook \
                -i /ansible/inventory.ini \
                -e backend_target=${backendTarget} \
                /ansible/switch-traffic.yml
                """

            }

        }

    }

    stage('Verify Active Production') {

        steps {

            sh '''
            echo "===== ACTIVE PRODUCTION ====="

            docker exec controller \
            ansible lb \
            -i /ansible/inventory.ini \
            -m shell \
            -a "curl -s http://localhost/api/"
            '''

        }

    }

    stage('Zero Downtime Verification') {

        steps {

            sh '''
            docker exec controller \
            ansible lb \
            -i /ansible/inventory.ini \
            -m shell \
            -a "for i in 1 2 3 4 5; do curl -s http://localhost/api/; echo; done"
            '''

        }

    }

}

post {

    success {

        echo 'BLUE-GREEN deployment completed successfully'

    }

    failure {

        echo 'Deployment failed'

    }

}


}
