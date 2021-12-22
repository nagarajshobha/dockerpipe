node {
    stage('scm checkout') {
        git credentialsId: 'github-cred', url: 'https://github.com/nagarajshobha/dockerpipe.git'
    }
    stage('maven'){
      def mavenHome = tool name: 'maven', type: 'maven'
      def mavenCmd = "${mavenHome}/bin/mvn"
      sh "${mavenCmd} clean package "
}
    stage('docker image'){
    sh 'docker build -t nagarajshobha/pipeline:3.0 .'
}
    stage('docker push'){
        withCredentials([string(credentialsId: 'docker-p', variable: 'dockerpwd')]) {
        sh "docker login -u nagarajshobha -p ${dockerpwd}"
}
     sh 'docker push nagarajshobha/pipeline:3.0'
    
}
   stage('ruuning conatiner on develpoer server'){
       def dockerRun = 'docker run --name pipelineapp2 -p 8080:8080 -d nagarajshobha/pipeline:3.0 '
       sshagent(['ssh-con']) {
           sh "ssh -o StrictHostKeyChecking=no ec2-user@13.59.38.98 ${dockerRun}"
           
}
   }
}
