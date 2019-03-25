# k8s kafka初始化顺序

修改了部分脚本让集群外也能访问kafka

### 测试下kubectl是不是好的
kubectl get nodes --insecure-skip-tls-verify=true

### kakfa和zk的hostpath的pvc
kubectl --insecure-skip-tls-verify=true apply -f configure/docker-storageclass-broker.yml
kubectl --insecure-skip-tls-verify=true apply -f configure/docker-storageclass-zookeeper.yml

### kafka命名空间
kubectl --insecure-skip-tls-verify=true apply -f 00-namespace.yml

### rbac策略，根据k8s集群配置应该是可选的

kubectl --insecure-skip-tls-verify=true apply -f rbac-namespace-default/node-reader.yml
kubectl --insecure-skip-tls-verify=true apply -f rbac-namespace-default/pod-labler.yml

### zk

kubectl --insecure-skip-tls-verify=true apply -f zookeeper/10zookeeper-config.yml
kubectl --insecure-skip-tls-verify=true apply -f zookeeper/20pzoo-service.yml
kubectl --insecure-skip-tls-verify=true apply -f zookeeper/21zoo-service.yml
kubectl --insecure-skip-tls-verify=true apply -f zookeeper/30service.yml
kubectl --insecure-skip-tls-verify=true apply -f zookeeper/50pzoo.yml
kubectl --insecure-skip-tls-verify=true apply -f zookeeper/51zoo.yml

### kafka

kubectl --insecure-skip-tls-verify=true apply -f kafka/10broker-config.yml
kubectl --insecure-skip-tls-verify=true apply -f kafka/20dns.yml
kubectl --insecure-skip-tls-verify=true apply -f kafka/30bootstrap-service.yml
kubectl --insecure-skip-tls-verify=true apply -f kafka/10broker-config.yml
kubectl --insecure-skip-tls-verify=true apply -f kafka/10broker-config.yml
kubectl --insecure-skip-tls-verify=true apply -f kafka/10broker-config.yml
kubectl --insecure-skip-tls-verify=true apply -f kafka/10broker-config.yml