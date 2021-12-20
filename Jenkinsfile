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
                    mkdir config_files
                    x=`ls -f ./*/*/*/*/*`
                    for f in $x ; do cp $f ./config_files/ ; done
                 '''
                 
                sshagent(['GitHub']){
                    sh '''
                        #!/bin/bash
                        git checkout configFiles
                        git status
                        git add ./config_files/*
                        commitMessage="Triggered Build: $BUILD_NUMBER"
                        git diff-index --quiet HEAD || git commit -m "${commitMessage}"
                        git push
                     '''
                    }
            }
        }
        
        
    }
    
    
}
