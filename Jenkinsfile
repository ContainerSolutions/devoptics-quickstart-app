node {
    stage ('checkout') {
        checkout scm
    }
    stage ('build') {
        withMaven(maven: 'maven-aotto') {
            sh "mvn clean install"
        }
        def dockerImage = docker.build("devoptics-quickstart-app:${env.BUILD_ID}")
        dockerImage.push()
    }
    stage ('fingerprint') {
        archiveArtifacts artifacts: "target/*.jar", fingerprint: true
    }
}
