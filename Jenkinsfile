pipeline {
    agent {
       label "build-server"
    }
    stages {
        stage('Build') {
            steps {
                //git branch: 'main', credentialsId: 'Github_cred', url: 'https://github.com/rahulmula/java-sample.git'
                sh '''
                pwd
                whoami
                git fetch https://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@github.com/rahulmula/java-sample.git
                wget https://download.java.net/java/GA/jdk13.0.1/cec27d702aa74d5a8630c65ae61e4305/9/GPL/openjdk-13.0.1_linux-x64_bin.tar.gz
                tar -xvf openjdk-13.0.1_linux-x64_bin.tar.gz
                sudo cp -r jdk-13.0.1 /opt/; sudo rm -r jdk-13.0.1
                JAVA_HOME='/opt/jdk-13.0.1'
                PATH="$JAVA_HOME/bin:$PATH"
                export PATH
                wget https://mirrors.estointernet.in/apache/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz
                tar -xvf apache-maven-3.6.3-bin.tar.gz
                sudo cp -r apache-maven-3.6.3 /opt/; sudo rm -r apache-maven-3.6.3
                M2_HOME='/opt/apache-maven-3.6.3'   
                PATH="$M2_HOME/bin:$PATH"
                export PATH
                pwd
                cd java-sample; mvn clean deploy -Dmaven.test.skip=true
                '''
                echo 'Building....'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn surefire-report:report'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
