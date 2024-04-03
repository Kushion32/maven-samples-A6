pipeline {
  agent any
  tools { 
      maven 'DHT_MAVEN' 
      jdk 'DHT_SENSE' 
  }
  stages{
  stage('Git Bisect') {
            steps {
                script {
                    sh 'git bisect start'
                    sh 'git bisect bad 198644632661c67b6c32f59e9047c11a70685e15'
                    sh 'git bisect good 98ac319c0cff47b4d39a1a7b61b4e195cfa231e5'
                    
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
                    
                    sh 'git bisect reset'
                }
            }
        }
  }
}