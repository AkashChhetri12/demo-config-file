pipeline {
    agent any

    stages {

        
        stage('Copying files') {
            environment {
                BUILD_NUMBER = "${env.BUILD_NUMBER}"
              }
            
            steps {
                
                 sh '''
                    #!/bin/bash
                    #mkdir -p config_files
                    #x=`ls -f ./*/*/*/*/*`
                    # for f in $x ; do cp $f ./config_files/ ; done
                    #git status
                    #git add ./config_files/*
                    #commitMessage="Triggered Build: $BUILD_NUMBER"
                    #git diff-index --quiet HEAD || git commit -m "${commitMessage}"
                    #git push --set-upstream origin configFiles
                    git checkout configFiles || git checkout -b configFiles
                    git checkout main /*/*/*/*/*
                 '''
                 

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
