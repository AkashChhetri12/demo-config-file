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
                        cd config_files
                        git init
                        git remote add origin git@github.com:AkashChhetri12/demo-config-file.git
                        git remote -v
                        git pull origin configFiles
                        ls -l
                        cd ..
                        x=`ls -f ./*/*/*/*/*`
                        for f in $x ; do cp $f ./config_files/ ; done
                        cd config_files
                        ls -l
                        git status
                        git add .
                        commitMessage="Triggered Build: $BUILD_NUMBER"
                        git diff-index --quiet HEAD || git commit -m "${commitMessage}"
                        git push origin HEAD:configFiles
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
