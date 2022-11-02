pipeline {
    agent any
    
    tools
    {
       maven "maven-3.8.1"
    }
     
    stages {
      stage('checkout') {
           steps {
             
                git branch: 'develop', url: 'https://github.com/mechsuzi497/anisble_ci.git'
             
          }
        }
         stage('Tools Init') {
            steps {
                script {
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
               def tfHome = tool name: 'Ansible'
                env.PATH = "${tfHome}:${env.PATH}"
                 sh 'ansible --version'
                    
            }
            }
        }
     
        
         stage('Execute Maven') {
           steps {
             
                sh 'mvn package'             
          }
        }
        
        
         
        
        
        
        stage('Ansible Deploy') {
             
            steps {
                 
             
               
               sh "ansible-playbook main.yml -i inventories/dev/hosts -- user jenkins --key-file ~/.ssh/id_rsa"

               
            
            }
        }
    }
}
