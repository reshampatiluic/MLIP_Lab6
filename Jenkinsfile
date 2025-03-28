pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh '''#!/bin/bash
                echo 'In C or Java, we can compile our program in this step'
                echo 'In Python, we can build our package here or skip this step'
                '''
            }
        }
        stage('Test') {
            steps {
                sh '''#!/bin/bash
                echo 'Test Step: We run testing tool like pytest here'

                # Initialize conda for Jenkins
                source $HOME/miniconda3/bin/activate

                # Create mlip environment if it doesn't exist
                if ! conda env list | grep -q mlip; then
                    conda create -n mlip python pytest numpy pandas scikit-learn -y -c conda-forge
                fi

                # Run pytest using conda run
                conda run -n mlip python -m pytest -v
                
                echo 'pytest completed successfully'
                '''
            }
        }
        stage('Deploy') {
            steps {
                echo 'In this step, we deploy our porject'
                echo 'Depending on the context, we may publish the project artifact or upload pickle files'
            }
        }
    }
}