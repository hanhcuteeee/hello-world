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
                    sh 'docker build -t hanh2002/helloworld:v1 .'
                    sh 'docker push hanh2002/helloworld:v1'
                }
            }
        }

        // stage('Deploy') {
        //     steps {
        //         sh "echo 12345"
        //     }
        // }


        stage('Deploy') {
            steps {
                sshagent(['ec2']) {
                    sh "
                    ssh -tt ec2-user@44.202.131.42
                    'docker pull hanh2002/helloworld:v1;
                    docker container stop nodejs-hello-world;
                    echo y | docker container prune;
                    docker container run -d --rm --name nodejs-hello-world -p 3000:3000 hanh2002/helloworld:v1'
                    "
                }
            }
        }
    }
    
    post {
        // Clean after build
        always {
            cleanWs()
        }
    }
}