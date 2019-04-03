pipeline {
    environment {
        ONE_VARIABLE = "1"
        TWO_VARIABLES = "2"
    }
    parameters {
        booleanParam defaultValue: false, description: 'There is no spoon.', name: 'THERE_IS_A_SPOON'
    }
    agent {
        label "master"
    }
    stages {
        /*
        First of all, who thought this comment was necessary?
        */
        stage("S1") {
            steps {
                echo "Not so basic now!"
            }
        }
        stage ("Intentional Merge Conflict via Parallel"){
            parallel {
                stage("S2") {
                    when {
                        expression {
                            echo "Expression returns true so netstat will run"
                            return true
                        }
                    }
                    steps {
                        sh "netstat -a"
                    }
                }
                stage ("in-parallel-1") {
                    steps{
                        echo "in-parallel-1"
                        sh "lsof"
                    }
                }
                stage ("in-parallel-2") {
                    steps{
                        echo "in-parallel-2"
                        sh "lsof"
                    }
                }
                stage ("in-parallel-3") {
                    steps{
                        echo "in-parallel-3"
                        sh "lsof"
                    }
                }
                stage ("in-parallel-4") {
                    steps{
                        echo "in-parallel-4"
                        sh "lsof"
                    }
                }
            } // end parallel block
        }
        stage("S1") {
            steps {
                echo "Basic Jenkinsfile"
            }
        }
        stage ("The old S2 was moved into the parallel block") {
            steps {
                echo "I will be surprised if this can be merged"
                sh "ps -ef"
            }
        }
        stage("S3") {
            steps {
                echo "Sleep 10 seconds"
                sleep 10
            }
        }
    }
}
