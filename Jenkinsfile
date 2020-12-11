pipeline {
    choice(name: 'test_name', choices: ['com.techprimers.testing.FizzBuzztest'], description: '')

    agent any

    stages {
        stage ('Compile Stage') {

            steps {
                withMaven(maven : 'maven_3_5_0') {
                    sh 'mvn clean compile'
                }
            }
        }

        stage ('Test if jar was generated properly') {
            steps {
                sh 'ls -A1 ./target'
            }
        }

        stage ('Testing Stage') {

            steps {
                withMaven(maven : 'maven_3_5_0') {
                    sh 'mvn test -Dtest=$test_name'
                }
            }
        }


        stage ('Deployment Stage') {
            steps {
                withMaven(maven : 'maven_3_5_0') {
                    sh 'mvn deploy'
                }
            }
        }
    }
    post {
        failure {
            echo 'Failed due authentication problems'
        }
    }
}