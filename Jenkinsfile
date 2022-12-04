podTemplate(yaml: '''
    apiVersion: v1
    kind: Pod
    metadata:
     name: kaniko-maven
     namespace: jenkins
    spec:
      containers:
      - name: maven
        image: maven:3.8.6-openjdk-18
        command:
        - sleep
        args:
        - 99d
      - name: kaniko
        image: gcr.io/kaniko-project/executor:debug-539ddefcae3fd6b411a95982a830d987f4214251
        volumeMounts:
        - name: kaniko-secret
          mountPath: /kaniko/.docker
      restartPolicy: Never
      volumes:
      - name: kaniko-secret
        secret:
            secretName: dockercred
            items:
            - key: .dockerconfigjson
              path: config.json
''') {
  node(POD_LABEL) {
    stage('Get a Maven project') {
      git url: 'https://github.com/Devops-dunia-company123/kubernetes-kaniko', branch: 'main'
      container('maven') {
        stage('Build a Maven project') {
          sh '''
          echo pwd
          '''
        }
      }
    }

    stage('Build Java Image') {
      container('kaniko') {
        stage('Build a Go project') {
          sh '''
            /kaniko/executor --context `pwd` --destination duniaalk/hello-kaniko:1.0
          '''
        }
      }
    }

  }
}
