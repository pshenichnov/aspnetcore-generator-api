// node {  
//     stage('Checkout') { 
//         git branch: 'pluralsight-pipeline-start', url: 'https://github.com/pshenichnov/aspnetcore-generator-api'
//     }
//     stage('Build') { 
//         sh 'docker build -t my-registry:55000/aspnetcore/generator:ci-$BUILD_NUMBER .'
//     }
// }

pipeline {

    environment {
        IMAGE = 'my-registry:55000/aspnetcore/generator:ci-${env.BUILD_NUMBER}'
    }

    agent any
    
    stages {
        stage('CI') {
            steps {
                git branch: 'pluralsight-pipeline-start', 
                    url: 'https://github.com/pshenichnov/aspnetcore-generator-api'
            
                //sh 'echo "IMAGE is $IMAGE"'
            
                sh 'docker build -t my-registry:55000/aspnetcore/generator:ci-$BUILD_NUMBER .'
            }
        }
    }
}

def notify(status){
    emailext (
      to: "pshenichnov@gmail.com",
      subject: "${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
      body: """<p>${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
        <p>Check console output at <a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a></p>""",
    )
}
