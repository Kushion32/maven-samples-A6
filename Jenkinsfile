pipeline {
  agent any
  tools { 
      maven 'DHT_MAVEN' 
      jdk 'DHT_SENSE' 
  }
  stage('Git Bisect') {
            steps {
                script {
                    // Initialize git bisect between known good and bad commits
                    sh 'git bisect start'
                    sh 'git bisect bad 198644632661c67b6c32f59e9047c11a70685e15'
                    sh 'git bisect good 98ac319c0cff47b4d39a1a7b61b4e195cfa231e5'
                    
                    // Use git bisect with a custom script that runs 'mvn clean test'
                    // The custom script should exit with 0 if successful, or with 1 if failed
                    sh """
                    git bisect run bash -c '
                    mvn clean test
                    if [ \$? -eq 0 ]; then
                        exit 0
                    else
                        exit 1
                    fi
                    '
                    """
                    // sh 'git bisect run mvn clean test'

                    // sh 'git bisect bad 8bad1c6db9cf6930abd8e52ff5dfdd046194ae9b'

                    // sh 'mvn clean test'

                    // sh 'git bisect bad 26438de182f7a00147b5e53e9408a3c3745ca509'

                    // sh 'mvn clean test'

                    // sh 'git bisect bad 8bad1c6db9cf6930abd8e52ff5dfdd046194ae9b'



                    
                    // Reset bisect after completion to clean up the bisect state
                    sh 'git bisect reset'
                }
            }
        }
  }