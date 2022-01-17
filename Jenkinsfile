node{

   stage("GIT Clone"){

      git credentialsId: 'GIT_SCT', url: 'https://github.com/pspk-ec-project/new_Jan_DEploy.git'
    }
    
   stage("Build Docker Images"){

        sh "docker build -t srinaths119/django . "
    }
    
   stage("Docker Push"){
       
      withCredentials([string(credentialsId: 'hub.docker_pswd', variable: '')]) {
    // some block
                     
          sh "docker login -u srinaths119 -p ${hub.docker_pswd}"
      }
   
       
       sh "docker push srinaths119/django"

     }

   stage("Deploy app in K8s cluster"){

     kubernetesDeploy(

        configs: 'django_deployment.yml',
        kubeconfigID: 'K8S_cluster_config',
        enableConfigSubstitution: true
          )

       }

}
