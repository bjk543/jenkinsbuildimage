node('master') {


    currentBuild.result = "SUCCESS"

    try {

       stage('Checkout'){
            checkout scm
       }
       
       stage('test'){
            sh 'npm install'
            sh 'npm test'
       }
       stage('build'){
            def customImage = docker.build("bjk543/nodeserver:1.0")
            customImage.inside {
                sh 'pwd'
            }
            customImage.push()
       }

    }
    catch (err) {

        currentBuild.result = "FAILURE"

            mail body: "project build error is here: ${env.BUILD_URL}" ,
            from: 'bjk543@gmail.com',
            replyTo: 'bjk543@gmail.com',
            subject: 'project build failed',
            to: 'bjk543@gmail.com'

        throw err
    }

}
