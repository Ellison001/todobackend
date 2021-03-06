node {
    checkout scm
    
    try {
        stage 'Run Unit/intergration tests'
        sh 'make test'
        
        stage 'Build application artifact'
        sh 'make build'
        
        stage 'Create release environment and run acceptance tests'
        sh 'make release'
        
        stage 'Tag and publish release image'
        sh "make tag latest \$(git rev-parse --short HEAD) \$(git tag --points-at HEAD)"
        sh "make buildtag master \$(git tag --points-at HEAD)"
        withEnv(["DOCKER_USER=${DOCKER_USER}",
                 "DOCKER_PASSWORD=${DOCKER_PASSWORD}"]) {
            sh 'make login'
        }
        
        sh "make publish"
    }
    
    finally {
        stage 'Collect test reports'
        echo 'Skip test reports at this moment.'
        stage 'Clean up'
        sh 'make clean'
        sh 'make logout'
    }
}
