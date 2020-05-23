pipeline {
agent any
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
        sh "./gradlew test jacocoTestCoverageVerification"
    }
}
}
}