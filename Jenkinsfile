pipeline {
    agent any

    stages {
        stage("Initial cleanup") {
            steps {
                deleteDir()
            }
        }

        stage('Checkout SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/lucm9/php-todo.git'
            }
        }

        stage('Prepare Dependencies') {
            steps {
                script {
                    def phpPath = sh(script: 'which php', returnStdout: true).trim()
                    def artisanPath = sh(script: 'which artisan', returnStdout: true).trim()

                    echo "PHP Path: ${phpPath}"
                    echo "Artisan Path: ${artisanPath}"

                    // Install Composer dependencies
                    sh 'composer install --no-interaction --prefer-dist'

                    // Run database migrations
                    sh "${phpPath} ${artisanPath} migrate --force"

                    // Seed the database (if needed)
                    // sh "${phpPath} ${artisanPath} db:seed --force"

                    // Generate the application key
                    sh "${phpPath} ${artisanPath} key:generate"
                }
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
