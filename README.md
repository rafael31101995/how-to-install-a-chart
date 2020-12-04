## __Dando uninstall em um realese nifi__
- Esse comando desinstala o nifi que se encontra dentro do namespace mundodocker.

        helm uninstall my-release -n mundodocker


## __Como instalar o nifi usando helm em um cluster kubernetes__

- Comando para instalação do nifi dentro do namespace mundodocker, onde o my-release representa o nome do nifi quando este estiver instalado dentro do mundodocker.

        helm install my-release cetic/nifi -n mundodocker

- Verificando o status do nifi dentro do namespace mundodocker

        helm status my-release -n mundodocker

- Verificando os pods criados pelo chart do nifi dentro do namespace mundodocker.
        
        kubectl get pods -n mundodocker

- Abrindo o nifi para ser acessado via localhost utilizando o port-forward.

        kubectl port-forward my-release-nifi-0 8080:8080 -n mundodocker

## __É possível configurar o seu próprio YAML file.__

## __Instale o helm chart do nifi utilizando um outro values.yaml.__

                helm install my-release cetic/nifi -n mundodocker --values=nifi-config-test.yml

## __Gerando os templates/receitas do cetic/nifi e incluindo na pasta ./yamls__

                helm template cetic/nifi --output-dir ./yamls

- Output do comando acima

        wrote ./yamls/nifi/charts/zookeeper/templates/poddisruptionbudget.yaml
        wrote ./yamls/nifi/charts/registry/templates/serviceaccount.yaml
        wrote ./yamls/nifi/charts/registry/templates/secret.yaml
        wrote ./yamls/nifi/templates/configmap.yaml
        wrote ./yamls/nifi/charts/registry/templates/service.yaml
        wrote ./yamls/nifi/charts/zookeeper/templates/svc-headless.yaml
        wrote ./yamls/nifi/charts/zookeeper/templates/svc.yaml
        wrote ./yamls/nifi/templates/service.yaml
        wrote ./yamls/nifi/templates/service.yaml
        wrote ./yamls/nifi/charts/registry/templates/statefulset.yaml
        wrote ./yamls/nifi/charts/zookeeper/templates/statefulset.yaml
        wrote ./yamls/nifi/templates/statefulset.yaml
        wrote ./yamls/nifi/charts/registry/templates/tests/test-connection.yaml

- O comando a seguir mostra como seria pegar os templates utilizando um outro values.

                helm template my-release cetic/nifi -n mundodocker --values=nifi-config-test.yml --output-dir ./yamls

- Output do comando acima

        wrote ./yamls/nifi/templates/configmap.yaml
        wrote ./yamls/nifi/templates/service.yaml
        wrote ./yamls/nifi/templates/service.yaml
        wrote ./yamls/nifi/templates/statefulset.yaml


## __Quantas replicas o nifi tera?__
## __O que é init container?__
## __Quantos init container ele faz dentro da imagem?__
## __Qual a ideia de volume dentro do kubernetes?__
## __Mencione três tipos de volumes.__

# Bibliografia

- [Como instalar o nifi usando helm.](https://github.com/cetic/helm-nifi)
- [Como instalar o kind, helm, kubectl.](https://github.com/rafael31101995/Kubernetes-basic-guide/blob/main/README.md)
- [Como criar pods e deployments.](https://www.mirantis.com/blog/introduction-to-yaml-creating-a-kubernetes-deployment/)
- [Alguns comando básicos do helm.](https://helm.sh/docs/intro/using_helm/)
- [Criando seu primeiro helm chart](https://docs.bitnami.com/tutorials/create-your-first-helm-chart/)
- [O que é o helm](https://www.youtube.com/watch?v=-ykwb1d0DXU)
- [Referencia para o comando helm template --output-dir](https://stackoverflow.com/questions/50584091/helm-export-yaml-files-locally-just-use-templating-engine-do-not-send-to-kuber)
