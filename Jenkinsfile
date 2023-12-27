pipeline {

    agent any

    stages {

        // stage('Build jar with maven') {
        //     steps {
        //         sh '''
        //             export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64 &&
        //             export PATH="/usr/lib/jvm/java-17-openjdk-amd64/bin:$PATH" &&
        //             echo $JAVA_HOME &&
        //             echo $PATH &&
        //             echo start build &&
        //             mvn clean package &&
        //             echo end build
        //         '''
        //     }
        // }

        stage('Build and push image') {
            steps {
                withDockerRegistry(credentialsId: 'hanh2002', url: 'https://index.docker.io/v1/') {
                    sh 'docker build -t hanh2002/hello-world:v1 .'
                    sh 'docker push hanh2002/hello-world:v1'
                }
            }
        }


        // stage('Deploy') {
        //     steps {
        //         sshagent(['ec2']) {
        //             sh "ssh -tt ec2-user@3.95.167.105 'echo 12345;whoami;ls -la'"
        //         }
        //     }
        // }
    }
    
    post {
        // Clean after build
        always {
            cleanWs()
        }
    }
}