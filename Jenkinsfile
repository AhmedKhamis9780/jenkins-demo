pipeline {
     agent any
    parameters {
        withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'CREDENTIALS', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']])
                        {
                            sh 'ant -Ddb.clean=${params.cleanDB} -Ddb.host=${params.host} -Ddb.userid=$USERNAME -Ddb.password=$PASSWORD'
                        }
        booleanParam(name:'project', defaultValue: true, description:'this paramater help you to know project name')
        choice(name: 'namespace', choices:['dev','prod','stage'], description: '' ) 
    }

    stages {
        stage('check') {
            steps {
                echo "checking your code"
                echo "${params.namespace}"
               
            }
        }

        stage('test') {
            when {
                expression{
                    params.project == true 
                }
            }
            steps {
                echo "testing your app" 
            }
        }
        
        stage('deployment') {  
            steps {
                echo "your code is deployed right now"
                echo "this build number $BUILD_NUMBER"
            }
        }    
    }

}
