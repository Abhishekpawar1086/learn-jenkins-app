pipeline {
    agent any
    environment {
        NETLIFY_SITE_ID = 'b1e9d291-d317-4eef-88ab-f29c2f0a4414'
    }

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
              }
            
            steps {
                sh '''
                   ls -la
                   node --version
                   npm --version
                   npm ci
                   npm run build
                   ls -la
                '''
            }
        }
        stage('Test') {
            steps {
                        sh'''
                        test -f build/index.html
                        '''
                    }
                }
        stage('Deploy staging') {
                    agent {
                        docker {
                            image 'node:18-alpine'
                            reuseNode true
                        }
                    }
                    steps {
                        sh '''
                           npm install netlify-cli
                           node_modules/.bin/netlify --version
                        '''
                    }
                
                }
                 stage('Approval') {
                    
                    steps {
                        input message: 'are you ready for build', ok: 'okay'
                    }
                
                }
                stage('Deploy prod') {
                    agent {
                        docker {
                            image 'node:18-alpine'
                            reuseNode true
                        }
                    }
                    steps {
                        sh '''
                           echo 'product'
                        '''
                    }
                
                } 
       
     }  
}



