pipeline {
environment {
  nameSpace="vcluster-bps-wp"
  nameVcluster="vcluster-bps-wp"
  }
  
  	agent {
    		kubernetes {
            cloud 'vcluster01'
      			inheritFrom 'default'
      			idleMinutes 5  // how long the pod will live after no jobs have run on it
      			yamlFile 'build-pod.yaml'  // path to the pod definition relative to the root of our project 
      			defaultContainer 'helm'  // define a default container if more than a few stages use it, will default to jnlp container
    		}
  	}
 
    stages {          
      stage('Deploy Vcluster-xxx ${nameVcluster} to K8S') {
             
            steps {
                echo 'Deploy RabbitMQ to Admin K8s Cluster ....'
              container('helm'){
                /* Funciona con el plugin de Kubernetes deployment de Azure -Actualmente tiene un bug-
                    script {
          		kubernetesDeploy (configs: 'deployment.yaml',kubeconfigId: 'kubeconfdigoce')
        		    }*/
        		    
        		    //workaround=> use helm hasta que actualicen el plugin kubernetesDeploy
        		    sh 'helm upgrade --install ${nameVcluster} vcluster --values vcluster.yaml --repo https://charts.loft.sh --namespace ${nameSpace}'
            }
             }   
           }
    }
}
