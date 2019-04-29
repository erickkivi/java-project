properties([pipelineTriggers([githubPush()])]) 

node('linux'){
    
    stage('Unit Test'){
        sh "ant -f test.xml -v"
        junit 'reports/result.xml'
    }
    
    stage('Build'){
        git 'https://github.com/rclc/java-project.git'
        sh "ant -f build.xml -v"
    }
    
    stage('Deploy'){
         sh "aws s3 cp dist/rectangle-${BUILD_NUMBER}.jar s3://BUCKET_NAME"
    }
    

    stage('Reports'){
       
    }
}
