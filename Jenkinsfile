pipeline {
    agent any

    stages {
        stage('Mirror') {
            steps {
                script {
                    sh 'git config --global core.sshCommand "ssh -o UserKnownHostsFile=/dev/null -o StrictHostKeyChecking=no"'
                    if (fileExists('testmirroring.git')) {
                        echo 'file exist'
                } else {
                        withCredentials([usernamePassword(credentialsId: 'bitbucket-jenkins-user', usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD')]) {
                            sh "git clone --mirror https://${GIT_USERNAME}:${GIT_PASSWORD}@bitbucket.org/codeonceteam/testmirroring.git"
                        }
                    }
                    sshagent(credentials: ['github-jenkins-user']) {
                        sh 'cd testmirroring.git'
                        sh 'git remote set-url --push origin git@github.com:Ayoubyoup/testmirror.git'
                        sh 'rm -fr "/var/lib/jenkins/jobs/testmirror/workspace/.git/rebase-apply"'
                        sh 'git pull --rebase git@github.com:Ayoubyoup/testmirror.git'
                        sh 'git push git@github.com:Ayoubyoup/testmirror.git HEAD:main'
                    }
                }
            }
        }
    }
}
