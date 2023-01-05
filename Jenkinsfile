pipeline {
    agent {
        docker {
            image 'cytopia/ansible'
        }
    }
    environment {
    ANSIBLE_KEY = credentials('ansible_VM')  
    ANSIBLE_HOST_KEY_CHECKING = false 
    }
    stages {
        stage('build') {
            steps {
                sh 'echo building ...'
                sh "which ansible || true"
                sh "ansible --version"
                sh "ansible-playbook --version"
                sh "ansible-galaxy --version"
                sh "ansible-galaxy collection install -r requirements.yml"
                sh "apk add --update --no-cache openssh sshpass"
                sh "ansible-playbook -i list.host -e ansible_ssh_pass=$ANSIBLE_KEY_PSW --ssh-common-args='-o StrictHostKeyChecking=no' playbook-b.yml"
            }
        }
    }
}
