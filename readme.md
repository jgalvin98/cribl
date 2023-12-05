Helm Install

export KUBECONFIG=/Users/gjay/workspace/projects/cribl/cribl-helm-test.yaml
helm repo add cribl https://criblio.github.io/helm-charts/
helm show values cribl/logstream-workergroup > values.yaml

** modify values.yaml

** create a namespace for cribl
kubectl create ns cribl

** override default PSA
kubectl label --overwrite ns cribl pod-security.kubernetes.io/audit=privileged 
kubectl label --overwrite ns cribl pod-security.kubernetes.io/warn=privileged


helm install logstream-wg cribl/logstream-workergroup -n cribl -f values.yaml



Create docker imagepullsecret to avoid ratelimit
kubectl create secret docker-registry regcred --docker-server=https://index.docker.io/v1/ --docker-username="jgalvin98" --docker-password="Charlie.Dog9901!" --docker-email="gjay@vmware.com" -n default


** uninstall cribl and reset PSA
helm uninstall logstream-wg -n cribl

** reset default PSA
kubectl label --overwrite ns cribl pod-security.kubernetes.io/audit=restricted 
kubectl label --overwrite ns cribl pod-security.kubernetes.io/warn=restricted


TMC:
Create GitRepo at CG or Ccluster level

https://github.com/criblio/helm-charts.git
