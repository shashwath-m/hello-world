node{
   stage('SCM Checkout'){
     git 'https://github.com/bhaskybuzz/hello-world.git'
   }
   stage('Compile-Package'){
      // Get maven home path
      def mvnHome =  tool name: 'M2_HOME', type: 'maven'   
      sh "${mvnHome}/bin/mvn package"
   }
   stage('SonarQube Analysis') {
        def mvnHome =  tool name: 'M2_HOME', type: 'maven''
        withSonarQubeEnv('sonar-6') 
          sh "${mvnHome}/bin/mvn sonar:sonar"
          }
   stage('Deploy to Tomcat'){
      sshagent(['tomcat-dev']) {
         sh 'scp -o StrictHostKeyChecking=no target/*.war ec2-user@172.31.92.65:/opt/apache-tomcat-8.5.54/webapps'
      }
   }
}
   
