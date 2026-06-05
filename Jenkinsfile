pipeline {
    agent any

    triggers {
        // Опрашивать GitHub на наличие новых коммитов каждую минуту
        pollSCM('* * * * *')
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Очищаем рабочую директорию перед сборкой
                cleanWs()
                // Скачиваем актуальный код из Git
                checkout scm
            }
        }

        stage('Docker Deploy') {
            steps {
                // Заходим во вложенную папку проекта, где лежит docker-compose.yml
                dir('team08-project') {
                    echo 'Перезапускаем контейнеры команды project_08...'
                    // Явно указываем имя проекта через -p, чтобы перетереть прошлый деплой
                    sh 'docker compose -p project_08 down'
                    sh 'docker compose -p project_08 up -d --build'
                }
            }
        }
    }
}