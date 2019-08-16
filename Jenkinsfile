pipeline {
  agent any
  stages {
    stage ('Lint HTML ') {
      steps {
        #!/bin/bash
        sh 'tidy -qe --doctype strict *.html'
      }
    }
    stage ('Quit if Lint HTML results in errors ') {
      steps {
        bash '''#!/bin/bash
                if [[ $(ls -A) ]]
                then break
                else continue
        	fi
        '''
      }
    }
    stage ('Upload to AWS ') {
      steps {
        withAWS(credentials: 'aws-static') {
          s3Upload(file:'index.html', bucket:'uniquenameproj4new', path:'index.html')
        }
      }
    }
  }
}
