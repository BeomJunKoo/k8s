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

