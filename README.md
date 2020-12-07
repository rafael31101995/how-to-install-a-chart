## __Como instalar o nifi usando helm em um cluster kubernetes__

- Comando para instalação do nifi dentro do namespace mundodocker, onde o my-release representa o nome do nifi quando este estiver instalado dentro do mundodocker.

        helm install my-release cetic/nifi -n mundodocker

- Verificando o status do nifi dentro do namespace mundodocker

        helm status my-release -n mundodocker

- Verificando os pods criados pelo chart do nifi dentro do namespace mundodocker.
        
        kubectl get pods -n mundodocker

- Abrindo o nifi para ser acessado via localhost utilizando o port-forward.

        kubectl port-forward my-release-nifi-0 8080:8080 -n mundodocker


## __Dando uninstall em um realese nifi__
- Esse comando desinstala o nifi que se encontra dentro do namespace mundodocker.

        helm uninstall my-release -n mundodocker


## __Instale o helm chart do nifi utilizando um outro values.yaml.__

- Mesmo comando de instalação do chart cetic/nifi porém utilizando outro values, no caso o nifi-config-test.yml.

                helm install my-release cetic/nifi -n mundodocker --values=nifi-config-test.yml

## __Gerando os templates/receitas do chart cetic/nifi e incluindo na pasta ./yamls__

- O comando a seguir mostra como seria pegar os templates utilizando um outro values.  

                helm template my-release cetic/nifi -n mundodocker --values=nifi-config-test.yml --output-dir ./yamls

- Output do comando acima

        wrote ./yamls/nifi/templates/configmap.yaml
        wrote ./yamls/nifi/templates/service.yaml
        wrote ./yamls/nifi/templates/service.yaml
        wrote ./yamls/nifi/templates/statefulset.yaml

+ Foram gerados 3 arquivos: 
  - configmap.yaml
    + explicação
  - service.yaml
    + explicação
  - statefulset.yaml
    + explicação



## __Subindo um novo nifi utilizando a receita obtida no ultimo comando rodado.__

- Necessário a utilização do comando apply, para cada um dos yamls gerados.

        kubectl apply -f configmap.yaml -n teste
        kubectl apply -f service.yaml -n teste
        kubectl apply -f statefulset.yaml -n teste

- Verificando se funcionou.

        kubectl port-forward my-release-nifi-0 8080:8080 -n teste


# Bibliografia

- [Como instalar o nifi usando helm.](https://github.com/cetic/helm-nifi)
- [Como instalar o kind, helm, kubectl.](https://github.com/rafael31101995/Kubernetes-basic-guide/blob/main/README.md)
- [Como criar pods e deployments.](https://www.mirantis.com/blog/introduction-to-yaml-creating-a-kubernetes-deployment/)
- [Alguns comando básicos do helm.](https://helm.sh/docs/intro/using_helm/)
- [Criando seu primeiro helm chart](https://docs.bitnami.com/tutorials/create-your-first-helm-chart/)
- [O que é o helm?](https://www.youtube.com/watch?v=-ykwb1d0DXU)
- [Referencia para o comando helm template --output-dir](https://stackoverflow.com/questions/50584091/helm-export-yaml-files-locally-just-use-templating-engine-do-not-send-to-kuber)
- [Kubernetes Architecture](https://blog.newrelic.com/wp-content/uploads/kubernetes_architecture.jpg)
- [So You Want To Configure The Perfect DB Cluster Inside A Kubernetes Cluster](https://medium.com/@tomerf/so-you-want-to-configure-the-perfect-db-cluster-inside-a-kubernetes-cluster-a4d2c26aca7a)
