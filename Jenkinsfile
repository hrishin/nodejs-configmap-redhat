#!/usr/bin/groovy
@Library('github.com/hrishin/osio-pipeline@load-resources')_

osio {
    config runtime: 'node'

    ci {
        def app = processTemplate()
        build app: app
    }

    cd {
     
      def resources = processTemplate(params: [
        release_version: "1.0.${env.BUILD_NUMBER}"
      ])

      def cm = loadResources(file: ".openshiftio/resource.configmap.yaml")
      echo "$cm"

      echo "$resources"
 
      echo "-------------- build default ----------------------------"
      build resources: resources
      
      echo "-------------- deploy stage-----------------------------------"
      deploy resources: [resources,  cm], env: 'stage'
    }
}

