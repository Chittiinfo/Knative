node('built-in') {
    stage('Continuous Download_Dev') {
    git branch: 'dev', url: 'https://github.com/Chittiinfo/knative.git'
}

stage('Continuous Build_Dev') {
    sh '''cd coit-frontend
docker build -t chittiinfo/coit-frontend:latest . -f Dockerfile-multistage '''
}

stage('Continuous Testing_Dev') {
    sh 'echo "This is sample Test"'
}

stage('Continuous Depolyment_Dev') {
    sh 'docker push chittiinfo/coit-frontend:latest'
}

stage('Continuous Delivery_Dev') {
    sh '''cd coit-frontend
kubectl apply -f "coit-frontendScaletoZero.yaml"
kn service update coit-frontend --image chittiinfo/coit-frontend:latest  --port 80 --scale-max 5 -n development
'''
}

}
