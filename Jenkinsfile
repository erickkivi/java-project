properties([pipelineTriggers([githubPush()])]) 

node('linux'){
    
    stage('Unit Test'){
        sh " ant -f test.xml -v
        junit 'reports/result.xml'
    }
    
    stage('Build'){
        git 'https://github.com/rclc/java-project.git'
        sh "ant"
        sh "ant -f build.xml -v"
    }
    
    

    stage('Reports'){
       
    }
}
