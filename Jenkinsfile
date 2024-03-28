pipeline {
    agent {
        node {
            label 'AGENT-1'
            }
        }
    options {
        ansiColor('xterm')
        // timeout(time: 1, unit: 'HOURS')
        // disableConcurrentBuilds()
    }    
    //build
    stages {
        stage ('VPC') {
            steps {
                sh """
                    cd 01-vpc
                    terraform init -reconfigure
                    terraform apply -auto-approve
                """    
            }
        }
        stage('VPN') {
            steps {
                sh """
                    cd 01-vpn
                    terraform init -reconfigure
                    terraform apply -auto-approve
                """
            }
        }
         stage('Example') {
            input {
                message "Should we continue?"
                ok "Yes, we should."
                submitter "alice,bob"
                parameters {
                    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                }
        stage ('DB ALB') {
            parallel {
                steps {
                    sh """
                        cd 04-databases
                        terraform init -reconfigure
                        terraform apply -auto-approve
                      """

                }
            }
        }
        stage ('APP ALB') {
            steps {
                sh """
                    cd 05-app-alb
                    terraform init -reconfigure
                    terraform apply -auto-approve
                """
            }
        }
        

    }

        //post build

        post {
            always {
                echo 'I will always say HareKrishna'
            }
            failure {
                echo 'it is failure'
            }
            success {
                echo 'it is success'
            }
        }
 }