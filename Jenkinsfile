node {
    
    // Clone the latest repo from the git....
    stage("Git Clone") {
        git branch: 'main', credentialsId: '2ba18c43-fb6f-402b-98ad-91664d4ceab5', url: 'https://github.com/sanjaysanju618/CDCI---Front-End---DotNet.git'
    }

    // Start building the dotnet env into the docker container....
    stage("Build DotNet") {
        try {
            // Remove the old container if not running....
            bat 'docker container stop dotapp'
            bat 'docker container rm dotapp'
            bat 'docker image rm dotapp'
        } catch(err) {
            bat 'echo Create new Dot Net Image'
        } finally {
            bat 'docker build --tag dotapp .'
        }
    }

    // Start the server or restart the server if running....
    stage("Start Server") {
        try {
            // Start the server on 5001 port....
            bat 'docker run -d -p 5001:80 --name dotapp dotapp'
        } catch (err) {
            // Restart the server if it is running....
            bat 'docker container restart dotapp'
        }
    }
}