#!/usr/bin/groovy

@Library('github.com/fabric8/osio-pipeline') _


osio {

  config runtime: 'node'

  ci {
     // override the RELEASE_VERSION template parameter
    def resources = processTemplate(params: [
        RELEASE_VERSION: "1.0.${env.BUILD_NUMBER}"
    ])
    def cm = loadResources(file: "service.yaml")
    // performs an s2i build
    build resources: resources    
    deploy resources: [resources,  cm], env: 'stage'
  }

  cd {

    // override the RELEASE_VERSION template parameter
    def resources = processTemplate(params: [
        RELEASE_VERSION: "1.0.${env.BUILD_NUMBER}"
    ])
    def cm = loadResources(file: ".openshiftio/service.yaml")

    // performs an s2i build
    build resources: resources
    deploy resources: [resources,  cm], env: 'stage'
    deploy resources: [resources,  cm], env: 'run', approval: 'manual'
  }
}
