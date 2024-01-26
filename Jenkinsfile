pipeline {
    agent any

    stages {
        stage("Initial cleanup") {
            steps {
                dir("${WORKSPACE}") {
                    deleteDir()
                }
            }
        }

        stage('Checkout SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/lucm9/php-todo.git'
            }
        }

        stage('Prepare Dependencies') {
            steps {
                sh 'composer install'
                sh 'php artisan migrate --force'
                sh 'php artisan db:seed'
                sh 'php artisan key:generate'
            }
        }

        // Uncomment the following stage if you have PHPUnit tests to run
        // stage('Execute Unit Tests') {
        //     steps {
        //         sh './vendor/bin/phpunit'
        //     }
        // }
    }
}
