pipeline{
    agent any 
stages {
    stage('Code checkout from github'){
    steps {
        echo '*******Code checkout*******'
        git url: "https://github.com/bhagyameka/codecoverage-report.git", credentialsId: 'c6947d68-906d-4126-a88a-d93c8d4a1ec8'
        echo '*******Code checkout done*******'
        echo '*******mvn version start*******'
        sh 'mvn --version'
        echo '*******mvn version end*******'
     
    }
}

stage ('Build using Maven') {
    steps {
        echo '*******mvn build start*******'
        sh "pwd"
       
      sh 'mvn clean install'
            echo '*******mvn build done*******'
    }
}

stage('unit testing') {
    steps {
        echo '*******unit testing starts*******'
        junit skipPublishingChecks: true, testResults: '**/target/surefire-reports/TEST-*.xml'   
        echo '*******unit testing ends*******'
               
    }
}
  stage ('jacoco report'){
        steps {
     jacoco maximumBranchCoverage: '70', maximumClassCoverage: '70', maximumComplexityCoverage: '70', maximumInstructionCoverage: '70', maximumLineCoverage: '70', maximumMethodCoverage: '70', minimumBranchCoverage: '50', minimumClassCoverage: '50', minimumComplexityCoverage: '50', minimumInstructionCoverage: '50', minimumLineCoverage: '50', minimumMethodCoverage: '50', runAlways: true
        }
    }
}
post{
    success{
        mail bcc: '', body: '''build succeeded
jacoco report generated''', cc: 'bhagyalakshmimeka26@gmail.com', from: '', replyTo: '', subject: 'build SUCCESS', to: 'bhagyakakumanu@gmail.com'
    }
}
}  
