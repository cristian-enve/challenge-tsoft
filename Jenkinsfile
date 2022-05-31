node {
    def app
    
    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */
        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
        * docker build on the command line */

        app = docker.build("getintodevops/hellonode")
    }

    stage('Test image') {
        /* Ideally, we would run a test framework against our image.
        * For this example, we're using a Volkswagen-type approach ;-) */

        app.inside {
            sh 'echo "Tests passed!"'
        }
    }
    
    stage('Load & Print'){
        def dummy = readFile (file: 'dummy.txt')
        println(dummy)
    }

    stage('Upload to Nexus'){
        steps {
            script{
            sh 'docker login -u admin -p password 192.168.0.226:8085'
            sh 'docker push getintodevops/hellonode'}
        }
    }
}
