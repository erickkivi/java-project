properties([pipelineTriggers([githubPush()])]) 

node('linux'){
    
    stage('Unit Test'){
        sh "ant -f test.xml -v"
        junit 'reports/result.xml'
    }
    
    stage('Build'){
        git 'https://github.com/erickkivi/java-project.git'
        sh "ant -f build.xml -v"
    }
    
    stage('Deploy'){
         sh "aws s3 cp dist/rectangle-${BUILD_NUMBER}.jar s3://elasticbeanstalk-us-east-1-405410764804"
    }
    

    stage('Reports'){
        
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'AWS user for Jenkins', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
            sh 'aws cloudformation describe-stack-resources --stack-name jenkins-stack --region us-east-1' 
        
    }
}
}
