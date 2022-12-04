pipeline {
    agent any

    stages {
        stage('Mirror') {
            steps {
                    sh 'git config --global core.sshCommand "ssh -o UserKnownHostsFile=/dev/null -o StrictHostKeyChecking=no"'
                withCredentials([usernamePassword(credentialsId: 'bitbucket-jenkins-user', usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD')]) {
                    sh 'rm -rf testmirroring.git'
                    sh "git clone --bare https://${GIT_USERNAME}:${GIT_PASSWORD}@bitbucket.org/codeonceteam/testmirroring.git"
                }
                sshagent(credentials: ['github-jenkins-user']) {
                    sh 'cd testmirroring.git'
                    sh 'git push --mirror git@github.com:Ayoubyoup/testmirror.git HEAD:main'
                }
            }
        }
    }
}
