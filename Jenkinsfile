// This should be our default master Jenkinsfile.
pipeline {
    environment {
        ONE_VARIABLE    = "1"
        TWO_VARIABLE    = "2"
        RED_VARIABLE    = "red"
        BLUE_VARIABLE   = "blue"
        BRANCH_VARIABLE = "master"
    }
    parameters {
        booleanParam defaultValue: true, description: 'Should we run netstat', name: 'SHOULD_I_NETSTAT'
    }
    agent {
        label "linux-remote"
    }
    stages {
        stage("Echo some env vars") {
            steps {
                echo "--> Our variables are ${env.ONE_VARIABLE}, ${env.TWO_VARIABLE}, ${env.RED_VARIABLE}, ${env.BLUE_VARIABLE}"
                echo "--> BRANCH_VARIABLE is ${env.BRANCH_VARIABLE}"
            }
        }
        stage("S1 netstat if param is true") {
            when {
                expression {
                    echo "Depends on the SHOULD_I_NETSTAT param"
                    return params.SHOULD_I_NETSTAT
                }
            }
            steps {
                sh "netstat -a"
            }
        }
        stage("master") {
            when {
                branch 'master'
            }
            steps {
                echo "--> HELLO FROM MASTER"
                sh "ls -alhR"
            }
        }
        stage("production") {
            when {
                branch 'production'
            }
            steps {
                echo "--> HELLO FROM PRODUCTION"
                sh "ls -alhR"
            }
        }
        stage("!= master") {
            when {
                not {
                    branch 'master'
                }
            }
            steps {
                echo "--> NOT MASTER"
                sh "ps -ef"
            }
        }
        stage("PR branch") {
            when {
                branch 'PR*'
            }
            steps {
                echo "--> PR Branch"
                echo "Change me to test merges"
                sh "du -h -d 1"
            }
        }
    }
}
