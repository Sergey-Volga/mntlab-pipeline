node('master') {
    stage('Init') {
        git branch: 'svolga', url: 'https://github.com/Sergey-Volga/mntlab-pipeline.git'
    }

    stage('Build') {
        sh 'gradle build'
    }

    stage('Test') {
        echo 'Test'
        parallel (
                'Unit Tests': {sh 'gradle test' },
                'Jacoco Tests': {sh 'gradle jacocoTestReport' },
                'Cucumber Tests': {sh 'gradle cucumber' },
        )
    }


    stage('Asking for manual approval') {
	input 'Deploy?'
    }

    stage ('Deployment') {
        sh 'java -jar gradle-simple.jar '
    }

    stage ('Sending status') {
        sh ' echo "SUCCESS" '
}
}
