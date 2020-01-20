pipeline {
    agent { node { label 'jenkins-worker-s1' } }

    options {
        buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '', numToKeepStr: '30'))

    }

    stages {
        stage('Prepare') {
            steps {
                dir('sonic-buildimage') {
                    checkout([$class: 'GitSCM',
                          branches: [[name: 'refs/heads/master']],
                          extensions: [[$class: 'SubmoduleOption',
                                        disableSubmodules: false,
                                        parentCredentials: false,
                                        recursiveSubmodules: false,
                                        reference: '',
                                        trackingSubmodules: false]],
                          userRemoteConfigs: [[url: 'http://github.com/Azure/sonic-buildimage']]])
                }
            }
        }

        stage('Build') {
            steps {
                echo "This is pipeline testing."
                sh 'echo "this is test"'
                sh '''
#!/bin/bash -xe
cat /etc/*release*
echo "This is the test build"
'''

            }
        }
    }
    post {
        cleanup {
            cleanWs(disableDeferredWipeout: false, deleteDirs: true, notFailBuild: true)
        }
    }
}