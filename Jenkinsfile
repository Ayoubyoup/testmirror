pipeline {
    agent any

    stages {
        stage('Mirror') {
            steps {
                // create ssh key credentials for jenkins
                //sshagent(credentials: ['BnCaZBzKi3PmGr+O5m6iTCRLBV7MgktdM2SWAZCplt8']) {
                //    sh 'git push --mirror https://github.com/Ayoubyoup/testmirror.git'
                //}
                withCredentials([usernamePassword(credentialsId: 'bitbucket-jenkins-user', usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD')]) {
                    sh 'rm -rf testmirroring.git'
                    sh "git clone --mirror https://${GIT_USERNAME}:${GIT_PASSWORD}@bitbucket.org/codeonceteam/testmirroring.git"
                }
                withCredentials([usernamePassword(credentialsId: 'github-jenkins-user', usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD')]) {
                    echo "${GIT_USERNAME}"
                    sh 'git remote rm origin'
                    sh "git remote add origin https://github.com/${GIT_USERNAME}/testmirror.git"
                    sh 'git push --mirror'
                }
            }
        }
    }
}
