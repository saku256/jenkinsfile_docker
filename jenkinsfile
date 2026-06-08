pipeline {
    agent any

    stages {
        stage('clone') {
    steps {
        // Pass both the URL and the branch inside the git command
        git url: 'https://github.com/saku256/demodockerfile.git', branch: 'main'
    }
}
    stage('build'){
        steps{
            // Run the build on a Unix agent. You must have Maven installed.
                sh 'docker build -t demodocker .'
        }
        
    }
    stage('push') {
    steps {
        sh 'docker tag demodocker sakshikulkarni256/kucl-0203:demodocker'
        
        // Everything that needs the credentials must live INSIDE this block
        withCredentials([usernamePassword(credentialsId: '5c716b10-00fb-487c-88f6-79909a1af8fd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
            
            // 1. Double quotes allow Jenkins to pass the variables
            // 2. The backslash (\$) safely escapes them for the shell
            // 3. --password-stdin hides your password from the build logs
            sh "echo \$PASS | docker login -u \$USER --password-stdin"
            
            // Pushing must also happen while authenticated inside the block
            sh 'docker push sakshikulkarni256/kucl-0203:demodocker'
        }
    }
}

    }
}
