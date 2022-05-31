pipeline{
    agent any
    stages{
        stage('Load & Print'){
            steps{
                script{
                    def dummy = readFile (file: 'dummy.txt')
                    println(dummy)
                }
            }
        }

        stage('Upload to Nexus'){
            steps{
                nexusPublisher nexusInstanceId: 'nexus', 
                nexusRepositoryId: 'challenge-tsoft', 
                packages: []
            }
        }
    }

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
                sh 'echo "Tests passed"'
            }
        }
    }
}