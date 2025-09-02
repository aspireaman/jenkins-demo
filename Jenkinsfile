pipeline {
  agent any

  environment {
    RAILS_ENV = 'test'
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Install Gems') {
      steps {
        sh 'bundle install --jobs=3 --retry=3'
      }
    }

    stage('DB Setup') {
      steps {
        sh 'bundle exec rake db:create db:migrate RAILS_ENV=test'
      }
    }

    stage('Run Tests') {
      steps {
        sh 'bundle exec rake test'
      }
    }

    stage('Deploy (Demo)') {
      when { branch 'main' }  // only run on main branch
      steps {
        echo "Pretending to deploy app to production..."
      }
    }
  }
}
