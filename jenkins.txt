pipeline{
    agent any
      environment {
          PATH = "$PATH;C:\\Users\\ShankarMadhavraoBhos\\maven\\apache-maven-3.8.6\\bin;C:\\Windows\\System32"
      }
        
        stages{
            stage('Checkout') {
            steps{
            echo "Checkout stage"
            echo"${params.browser}"
            git credentialsId: '8008faf8-9055-4db2-895b-80ff4ea9fcb2', url: 'https://github.com/ShankarB98/sonarintegrationrepo1.git'
            }
                
            }
            stage('test')
            {
             echo "test stage"
             sh "mvn test -Dbrowser = ${params.browser} -Dplatform = ${params.platform}"
            
            }
        }

       
    post {
      always
      {
       echo "Artifact"
       archiveArtifacts artifacts: 'report/TS_01.html', followSymlinks: false
        
      
      
    }
}
}

