node('built-in') {
    stage('Continuous Download_Prod') {
    git branch: 'prod', url: 'https://github.com/Chittiinfo/knative.git'
}

stage('Continuous Build_Prod') {
    sh '''cd coit-frontend
docker build -t chittiinfo/coit-frontend:${APP_VERSION} . -f Dockerfile-multistage '''
}

stage('Continuous Testing_Prod') {
    sh 'echo "This is sample Test"'
}

stage('Continuous Depolyment_Prod') {
    sh 'docker push chittiinfo/coit-frontend:${APP_VERSION}'
}

stage('Continuous Delivery_Prod') {
    sh '''cd coit-frontend
kubectl apply -f "coit-frontendScaletoZero.yaml"
kn service update coit-frontend --image chittiinfo/coit-frontend:${APP_VERSION}  --port 80 --scale-min 5 --scale-max 100 -n prod
'''
}

}
