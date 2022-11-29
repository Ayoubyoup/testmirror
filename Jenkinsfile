pipeline {
    agent any

    stages {
        stage('Mirror') {
            steps {
                // create ssh key credentials for jenkins
                //sshagent(credentials: ['BnCaZBzKi3PmGr+O5m6iTCRLBV7MgktdM2SWAZCplt8']) {
                //    sh 'git push --mirror https://github.com/Ayoubyoup/testmirror.git'
                //}
                
                sh "git remote set-url origin https://github.com/Ayoubyoup/testmirror.git"
                sh "git push -–mirror https://github.com/Ayoubyoup/testmirror.git"
            }
        }
    }
}
