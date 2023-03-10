# k8s
kubenetes study 
 
---

## k8s cluster
- master node 
- etcd cluster
- kube-apiserver 
- kube-scheduler

### master node
역할 : 
manage, plan, schedule, monitor, nodes


### 1. etcd (master node)
nodes / pods / configs / secrets / accounts / roles / bindings / others 등의 정보를 저장


etcd.service install 
> advertise-clinet-urls https://${INTERNAL_IP}:2379 

   : etcd 리슨 포트 (default port : 2379) 

> initial-cluster controller-0=https://${CONTROLLER0_IP}:2380,controller-1=https://${CONTROLLER1_IP}:2380 

   : 클러스터에 여러 마스터 노드를 설정하여 etcd 분산 구성 (etcd HA 환경 구성 내용) 


### 2. qadium 
: 모의고사 방식 내용

### kubeadm
> kubectl get pods -n kube-system 

: pod 명령어를 통해 etcd 데이터베이스를 조회 가능

kube-apiserver 동작

```
예시) 생성 과정 
1) 인증된 사용자가 작업 요청
2) kube-apiserver 요청 확인
3) etcd cluster 서버의 정보 업데이트
4) result "Pod created!" 결과 확인
5) kube-scheduler 는 kube-apiserver를 모니터링하여 위의 결과에 대한 변경 사항 발생 내용 확인
6) kube-scheduler 는 새로운 pod 내용을 배포하기 위해 kube-apiserver 요청 내용 전달
7) woker nodes 에 컨테이너 런타임 엔진에 요청 내용 지시하여 애플리케이션 배포
8) kubelet 은 kube-apiserver 상태 업데이트하고 etcd 클러스터로 정보 업데이트 최종 수행
```
### kube Controller-Manager
- 지속적인 감시 (watch Status)  

> Node Monitor Period = 5s 

: kube-apiserver 를 통해 (5초)마다 node-Controller의 하트비트 상태 확인 옵션

> Node Monitor Grace Period = 40s

: 노드가 연결할 수 없는 상태로 표시되기 까지의 상태 (40초) 기다리는 옵션 

> POD Eviction Timeout = 5m 

: 연결할 수 없는 상태를 확인하고 (5분) 후 할당된 POD 제거 옵션 


kube Controller-Manager 서비스 설정 경로
> /etc/systemd/system/kube-controller-manager.service

적용 확인  
> /etc/kubernets/manifests/kube-controller-manager.yaml

Replication-Controller 

: POD 죽은 경우 POD를 생성합니다.

### Kube-Scheduler
어떤 POD가 어떤 노드로 보낼지 결정하기 위한 역할
(실제 POD의 배치는 kubelet이 수행합니다.)

kube-scheduler.service install 

kube-scheduler 서비스 설정 경로
> /etc/kubernetes/manifests/kube-scheduler.yaml 

### kubelet
Worker Nodes 에서 Master Node와 유일한 접점 (선장)

### kube proxy
수행 방식 : iptables 규칙을 사용 
kubernetes cluster 내에서 모든 POD는 다른 모든 POD에 도달 가능합니다. 

활용 내용

- 어플리케이션의 노드 배치
- 배포된 데이터베이스 응용 프로그램

통신 예시) 

서비스 IP(10.96.12) -> POD IP(10.32.0.14, 10.32.0.15) 


## Yaml in Kubernetes
필수 포함 내용
- apiVersion: 

: 개체 생성에 사용하는 Kubernetes API 버전 지정 내용
- kind: 
- metadata: 
- spec: 

