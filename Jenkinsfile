pipeline{
    agent any

    stages{

        stage('Build Dokcer Images'){
            steps{
                sh '''. ~/.bashrc
                        docker-compose build
                        docker-compose push
                        '''
            }
        }
        
        
        stage('Deploy Services'){
            steps{
                sh '''ssh jenkins@35.223.251.82 << BOB
                        export BUILD_NUMBER='${BUILD_NUMBER}'
                        docker service update --replicas 3 --image 35.228.228.71:5000/countries_service:-${BUILD_NUMBER} microservices_countries
                        docker service update --replicas 2 --image 35.228.228.71:5000/frontend_service:-${BUILD_NUMBER} microservices_frontend
                        docker service update --replicas 2 --image 35.228.228.71:5000/prize_service:-${BUILD_NUMBER} microservices_prize
                        docker service update --replicas 2 --image 35.228.228.71:5000/temperature_service:-${BUILD_NUMBER} microservices_temperature
                        '''
            }
        }
        /*
        stage('Container Replicas'){
            steps{
                sh '''ssh jenkins@35.223.251.82 << BOB
                    export BUILD_NUMBER='${BUILD_NUMBER}'
                    docker service update --replicas 3 microservices_countries
                    docker service update --replicas 2 microservices_frontend
                    docker service update --replicas 2 microservices_prize
                    docker service update --replicas 2 microservices_temperature
                    '''
            }
        }
        */
    }
}
