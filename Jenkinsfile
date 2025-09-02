pipeline {
  agent any   // Run directly on Jenkins host

  environment {
    RAILS_ENV = "test"
    BUNDLE_PATH = "vendor/bundle"
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Install Dependencies') {
      steps {
        sh '''
          gem install bundler || true
          bundle install --path vendor/bundle
        '''
      }
    }

    stage('DB Setup') {
      steps {
        sh '''
          bundle exec rails db:drop db:create db:migrate RAILS_ENV=test
        '''
      }
    }

    stage('Run Tests') {
      steps {
        sh 'bundle exec rails test'   // or rspec if you use rspec
      }
    }

    stage('Assets Precompile') {
      steps {
        sh 'bundle exec rails assets:precompile'
      }
    }

    stage('Deploy (Simulated)') {
      steps {
        echo "🚀 Deploy step would go here (Capistrano, copy files, restart service, etc.)"
      }
    }
  }
}
