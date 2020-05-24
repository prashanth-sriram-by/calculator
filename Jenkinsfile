pipeline {
agent any
triggers {
    pollSCM('15 * * * *')
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
        sh "./gradlew checkstyleMain"
    }
}
}

}