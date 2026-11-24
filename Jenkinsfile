pipeline {
    agent none
    stages {
        stage('Build-2') {
            agent {
                label 'build'
            }
            
            steps {
                deleteDir()
                
                sh'''
                git clone https://github.com/Razinmd/git-test.git
                ls -la
                '''
                
                stash name: 'webpage', includes: 'git-test/**'
            }
        }
        stage('Deploy-ssh'){
            agent {
                label 'deploy'
            } 
            steps {
                deleteDir()
                
                unstash 'webpage'
                sh '''
                sudo rm -rf /var/www/html/*
                sudo cp -r git-test/* /var/www/html/
                ls -la /var/www/html/
                '''
            }
        }
    }
}
