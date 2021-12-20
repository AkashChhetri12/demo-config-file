pipeline {
    agent any

    stages {

        
        stage('Copying files') {
            environment {
                BUILD_NUMBER = "${env.BUILD_NUMBER}"
              }
            
            steps {

                sshagent(['GitHub']){
                    sh '''
                        #!/bin/bash
                        mkdir config_files
                        git ls-remote git@github.com:AkashChhetri12/demo-config-file.git
                        git remote set-url origin git@github.com:AkashChhetri12/demo-config-file.git
                        git remote -v
                        git checkout main || git checkout -b main
                        git checkout configFiles || git checkout -b configFiles
                        #git pull origin configFiles
                        ls -l
                        working=`pwd`
                        x=`ls -f $working/*/*/*/*/*`
                        for f in $x ; do git checkout main -- ${f#"$working/"} ; done
                        ls -al
                        git status
                        commitMessage="Triggered Build: $BUILD_NUMBER"
                        git diff-index --quiet HEAD || git commit -m "${commitMessage}"
                        git push --set-upstream origin configFiles
                     '''
                    }

            }
        }    
        
    }
    post {
            always {
                echo 'One way or another, I have finished'
                deleteDir() /* clean up our workspace */
            }
        }
    
}
