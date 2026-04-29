pipeline {
	agent any

	stages {
		stage('Checkout') {
			steps {
				git branch: 'main', url: 'https://github.com/SebBear0/8.2CDevSecOps.git'
			}
		}

		stage('Install Dependencies') {
			steps {
				sh 'nix develop --command npm install'
			}
		}

		stage('Run Tests') {
			steps {
				sh 'nix develop --command npm test || true' // Allows pipeline to continue despite test failures
			}
		}

		stage('Generate Coverage Report') {
			steps {
				// Ensure coverage report exists
				sh 'nix develop --command npm run coverage || true'
			}
		}

		stage('NPM Audit (Security Scan)') {
			steps {
				sh 'nix develop --command npm audit || true' // This will show known CVEs in the output
			}
		}

	} 
} 
