stage 'CI'
    node {
        checkout scm   
    
        //git branch: 'jenkins2-course', 
        //    url: 'https://github.com/fdacumos/solitaire-systemjs-course.git'
    
        // pull dependencies from npm
        // on windows use: bat 'npm install'
        //sh 'npm install'
        bat 'npm install'
    
        // stash code & dependencies to expedite subsequent testing
        // and ensure same code & dependencies are used throughout the pipeline
        // stash is a temporary archive
        stash name: 'everything', 
              excludes: 'test-results/**', 
              includes: '**'
              
        // test with PhantomJS for "fast" "generic" results
        // on windows use: bat 'npm run test-single-run -- --browsers PhantomJS'
        //sh 'npm run test-single-run -- --browsers PhantomJS'
        bat 'npm run test-single-run -- --browsers PhantomJS'
        
        // archive karma test results (karma is configured to export junit xml files)
        step([$class: 'JUnitResultArchiver', 
              testResults: 'test-results/**/test-results.xml'])
              
    }


stage('Browser Testing')
parallel chrome: {
    echo 'Chrome Testing Here'
}, firefox: {
    echo 'Firefox Testing Here'
}, safari: {
    echo 'Safari Testing Here'
}

node {
    notify('Deploy to staging?')
}

input 'Deploy to staging?'

stage name: 'Deploy', concurrency: 1
node {
    echo 'Deploy here...'
}

def notify(status){
    emailext (
      to: "fdacumos@legalzoom.com",
      subject: "${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
      body: """<p>${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
        <p>Check console output at <a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a></p>""",
    )
}









def notify(status){
    emailext (
      to: "wesmdemos@gmail.com",
>>>>>>> 57f1ed0b1a1f44509550a822835f700d35892260
      subject: "${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
      body: """<p>${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
        <p>Check console output at <a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a></p>""",
    )
}
