node {
    stage("Git Clone") {
        git branch: 'main', credentialsId: '2ba18c43-fb6f-402b-98ad-91664d4ceab5', url: 'https://github.com/sanjaysanju618/CDCI---Front-End---DotNet.git'
    }
    stage("Build DotNet") {
        try {
            bat 'docker container stop dotapp'
            bat 'docker container rm dotapp'
            bat 'docker image rm dotapp'
        } catch(err) {
            bat 'echo Create new Image'
        } finally {
            bat 'docker build --tag dotapp .'
        }
    }
    stage("Start Server") {
        try {
            bat 'docker run -d -p 5001:80 --name dotapp dotapp'
        } catch (err) {
            bat 'docker container restart dotapp'
        }
    }
}