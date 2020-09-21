node {
    def mvnHome
    stage('Preparation') { // for display purposes
        // Get some code from a GitHub repository
        git 'https://github.com/vardansavarde/SimpleJavaWebApp.git'
        // Get the Maven tool.
        mvnHome = tool 'Maven 3.3.3'
    }
    stage('Build') {
        // Run the maven build
        withEnv(["MVN_HOME=$mvnHome"]) {
            if (isUnix()) {
                sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean package'
            } else {
                bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)
            }
        }
    }
    stage('Results') {
        junit allowEmptyResults: true,testResults: '**/target/surefire-reports/TEST-*.xml'
        archiveArtifacts 'target/*.war'
    }
}
