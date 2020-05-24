pipeline {
agent any
triggers {
    pollSCM('* * * * *')
}
stages {
stage("Compile") {
    steps {
        sh "./gradlew compileJava"
    }
}
stage("UnitTests") {
    steps {
        sh "./gradlew test"
    }
}
stage("CodeCoverage") {
    steps {
        sh "./gradlew jacocoTestReport"
        publishHTML (target: [
        reportDir: 'build/reports/jacoco/test/html',
        reportFiles: 'index.html',
        reportName: "JaCoCo Report"
        ])
        sh "./gradlew jacocoTestCoverageVerification"
    }
}
stage("Static code analysis") {
    steps {
    publishHTML (target: [
    reportDir: 'build/reports/checkstyle/',
    reportFiles: 'main.html',
    reportName: "Checkstyle Report"
    ])
        sh "./gradlew checkstyleMain"
    }
}
}
post {
    always {
    mail to: 'prashanthsriram145@gmail.com',
    subject: "Completed Pipeline: ${currentBuild.fullDisplayName}",
    body: "Your build completed, please check: ${env.BUILD_URL}"
}}
}