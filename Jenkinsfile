node('docker') {
    env.PROJECT_NAME = getProjectName("${env.JOB_NAME})")
    sh 'env'
    stage 'Checkout'
    // Get some code from a GitHub repository
    checkout scm

    stage 'Build'
    // Build Docker image
    def image = docker.build("$env.PROJECT_NAME-$env.BRANCH_NAME:${env.BUILD_NUMBER}")

    stage 'Test'
    stage 'Production'
    // Tag image as latest if builds are build from master
    if ('master'.equalsIgnoreCase("$env.BRANCH_NAME")) {
        image.tag("$env.PROJECT_NAME:${env.BUILD_NUMBER}")
    }
}

def static String getProjectName(def String jobName) {
    def String[] jobCoordinates = jobName.tokenize('/')
    def result = jobCoordinates[1] != null ? jobCoordinates[1] : jobName
    return result;
}
