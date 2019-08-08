node{
	stage('SCM Checkout'){
		git branch: 'smtpjenkins', url: 'https://github.com/spoudel2/devopsprojects.git'
	}
	stage('Compile-Package'){
		def mvnHome = tool name: 'maven', type: 'maven'
		sh "${mvnHome}/bin/mvn package"
	}
	stage('Deploy to Tomcat'){
		sshagent(['tom-dev']) {
		sh 'scp -o StrictHostKeyChecking=no target/*.war ec2-user@54.89.134.131:/opt/tomcat9/webapps/'
		}
	}
	stage('Slack Notification'){
	slackSend baseUrl: 'https://hooks.slack.com/services/', channel: '#jenkinslab', color: '#439FE0', message: 'New Build deployed', teamDomain: 'intelycore8', tokenCredentialId: 'slack-secret'
	}
	stage('Email Notification'){
	mail bcc: '', body: 'This is body', cc: '', from: 'rock.sagar234@gmail.com', replyTo: 'rock.sagar234@gmail.com', subject: 'This is Subject', to: 'rock.sagar234@gmail.com'
	}

}

