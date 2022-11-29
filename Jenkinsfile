pipeline{
    agent{
        docker {
            image 'maven:3.8.1-adoptopenjdk-11'
            args '-v /root/.m2:/root/.m2'
        }
    }
    
    options{
        skipStagesAfterUnstable()
    }

    stages{
        stage("Build"){
            steps{
                echo "========Building Java Project========"
                sh 'mvn -B -DskipTests clean package'
            }
            post{
                always{
                    echo "========always========"
                }
                success{
                    echo "========A executed successfully========"
                }
                failure{
                    echo "========A execution failed========"
                }
            }
        }

        stage("Test"){
            steps{
                echo "========Testing the Java Project========"
                sh 'mvn test'
            }
            post{
                always{
                    echo "========always========"
                    junit "target/surefire-reports/*.xml"
                }
                success{
                    echo "========A executed successfully========"
                }
                failure{
                    echo "========A execution failed========"
                }
            }
        }

        stage("Deploy"){
            steps{
                echo "========Deploying the Java Project========"
                sh './jenkins/scripts/deliver.sh'
            }
            post{
                always{
                    echo "========always========"
                }
                success{
                    echo "JAR created succesfully"
                }
                failure{
                    echo "========A execution failed========"
                }
            }
        }

    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}