pipeline {
    agent any

    stages {
        stage('Mirror') {
            steps {
                // create ssh key credentials for jenkins
                //sshagent(credentials: ['BnCaZBzKi3PmGr+O5m6iTCRLBV7MgktdM2SWAZCplt8']) {
                //    sh 'git push --mirror https://github.com/Ayoubyoup/testmirror.git'
                //}
                    sh 'git config --global core.sshCommand "ssh -o UserKnownHostsFile=/dev/null -o StrictHostKeyChecking=no"'
                withCredentials([usernamePassword(credentialsId: 'bitbucket-jenkins-user', usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD')]) {
                    sh 'rm -rf testmirroring.git'
                    sh "git clone --mirror https://${GIT_USERNAME}:${GIT_PASSWORD}@bitbucket.org/codeonceteam/testmirroring.git"
                }
                sshagent(credentials: ['github-jenkins-user']) {
                    sh 'cd testmirroring.git'
                    sh 'git remote set-url --push origin git@github.com:Ayoubyoup/testmirror.git'
                    sh 'git pull --rebase'
                    sh 'git push --mirror'
                }
            }
        }
    }
}
