
node {

    def mavenHome = tool name: "Mavne-3.9.6"

    stage('git checkout') {
        git branch: 'master',
            url: 'https://github.com/vineete2/maven-webapplication-project-kkfunda.git'
    }

    stage('compile') {
        sh "${mavenHome}/bin/mvn compile"
    }

    stage('build') {
        sh "${mavenHome}/bin/mvn clean package"
    }

    stage('Sonar') {
        sh "${mavenHome}/bin/mvn sonar:sonar"
    }

    stage('Nexus') {
        sh "${mavenHome}/bin/mvn clean deploy"
    }

    stage('Deploy to Tomcat') {
        sh """
            curl -u kk:password \
            --upload-file target/maven-web-application.war \
            "http://65.0.178.196:8080/manager/text/deploy?path=/maven-web-application&update=true"
        """
    }

} // End of node
