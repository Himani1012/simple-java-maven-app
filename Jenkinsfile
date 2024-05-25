pipeline {
    agent any
    stages {
        stage('Build') { 
            steps {
                withMaven(
                    // Maven installation declared in the Jenkins "Global Tool Configuration"
                    maven: 'maven', // (1)
                    // Use `$WORKSPACE/.repository` for local repository folder to avoid shared repositories
                    mavenLocalRepo: '.repository', // (2)
                    // Maven settings.xml file defined with the Jenkins Config File Provider Plugin
                    // We recommend to define Maven settings.xml globally at the folder level using
                    // navigating to the folder configuration in the section "Pipeline Maven Configuration / Override global Maven configuration"
                    // or globally to the entire master navigating to  "Manage Jenkins / Global Tools Configuration"
                    // mavenSettingsConfig: 'my-maven-settings' // (3)
                ) {
                  // Run the maven build
                  sh 'mvn -B -X -DskipTests clean package'
                } 
            }
        }
        stage('Test') {
            steps {
                withMaven(
                    // Maven installation declared in the Jenkins "Global Tool Configuration"
                    maven: 'maven', // (1)
                    // Use `$WORKSPACE/.repository` for local repository folder to avoid shared repositories
                    mavenLocalRepo: '.repository', // (2)
                    // Maven settings.xml file defined with the Jenkins Config File Provider Plugin
                    // We recommend to define Maven settings.xml globally at the folder level using
                    // navigating to the folder configuration in the section "Pipeline Maven Configuration / Override global Maven configuration"
                    // or globally to the entire master navigating to  "Manage Jenkins / Global Tools Configuration"
                    // mavenSettingsConfig: 'my-maven-settings' // (3)
                ) {
                    sh 'mvn test'
                }
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Code Quality Analysis') {
            steps {
                withMaven(
                        // Maven installation declared in the Jenkins "Global Tool Configuration"
                        maven: 'maven', // (1)
                        // Use `$WORKSPACE/.repository` for local repository folder to avoid shared repositories
                        mavenLocalRepo: '.repository', // (2)
                        // Maven settings.xml file defined with the Jenkins Config File Provider Plugin
                        // We recommend to define Maven settings.xml globally at the folder level using
                        // navigating to the folder configuration in the section "Pipeline Maven Configuration / Override global Maven configuration"
                        // or globally to the entire master navigating to  "Manage Jenkins / Global Tools Configuration"
                        // mavenSettingsConfig: 'my-maven-settings' // (3)
                    ) {
                        withSonarQubeEnv() {
                          sh "mvn clean verify sonar:sonar -Dsonar.projectKey=simple-java-maven-app -Dsonar.projectName='simple-java-maven-app'"
                        }
                    }
              }
        }
    }
}
