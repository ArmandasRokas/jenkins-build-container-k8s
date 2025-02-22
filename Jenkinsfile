podTemplate(yaml: '''
              kind: Pod
              spec:
                containers:
                - name: kaniko
                  image: gcr.io/kaniko-project/executor:debug
                  command:
                  - sleep
                  args:
                  - 99d
'''
  ) {

  node(POD_LABEL) {
    stage('Build and push container image') {
      git branch: 'main',  url: 'https://github.com/ArmandasRokas/jenkins-build-container-k8s.git'
      container('kaniko') {
        sh "/kaniko/executor -f `pwd`/Dockerfile -c `pwd` --insecure --skip-tls-verify --cache=true --destination=192.168.8.110:5000/custom-nginx:${BUILD_ID}"
      }
    }
  }
}
