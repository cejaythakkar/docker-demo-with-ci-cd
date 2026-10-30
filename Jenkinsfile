pipeline{
    agent any

    environment{
        FRONTEND_IMAGE= "mern-frontend:jenkins"
        BACKEND_IMAGE= "mern-backend:jenkins"
        SERVER_PORT="5555"
        VITE_API_URL="/api"
        CLIENT_PORT="80"
        MONGODB_URI="mongodb://mongo:27017/intro-to-docker"
        DOCKERHUB_USERNAME="cejaythakkar07"
    }

    stages{
        stage('checkout code'){
            steps {
                git url : 'https://github.com/cejaythakkar/docker-demo-with-ci-cd.git',branch: 'main'
            }
        }
        stage('Prepare .env'){
            steps{
                sh '''
                    mkdir -p server
                    cat > server/.env <<EOF
                    PORT=$SERVER_PORT
                    MONGODB_URI=$MONGODB_URI
                    EOF
                '''
            }
        }

        stage('Build docker images'){
            steps{
                sh '''
                    echo "building backend image..."
                    docker build -t $BACKEND_IMAGE ./server

                    echo
                    echo "building frontend image..."
                    docker build -t $FRONTEND_IMAGE ./client --build-arg VITE_API_URL=http://localhost:5555/api
                '''
            }
        }

        stage('run images with docker compose'){
            steps{
                sh '''
                    echo "Starting MERN app with docker componse"
                    docker compose up -d
                    echo "showing running containers"
                    docker ps
                '''
            }
        }
    }
}
