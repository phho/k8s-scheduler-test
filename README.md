# k8s-scheduler-test
```bash
kubectl apply -f custom-scheduler.yml -n kube-system
kubectl create rolebinding -n kube-system crl:apiserver --role=extension-apiserver-authentication-reader --serviceaccount=kube-system:crl-scheduler
kubectl rollout restart deployment/crl-scheduler -n kube-system

root@DESKTOP-H1BKVCJ:~/crl-scheduler/deploy# kubectl logs deploy/crl-scheduler -n kube-system -f
I0716 17:25:31.738218       1 serving.go:319] Generated self-signed cert in-memory
I0716 17:25:32.335094       1 server.go:148] Version: v0.0.0-master+$Format:%h$
I0716 17:25:32.335189       1 defaults.go:91] TaintNodesByCondition is enabled, PodToleratesNodeTaints predicate is mandatory
W0716 17:25:32.347015       1 authorization.go:47] Authorization is disabled
W0716 17:25:32.347136       1 authentication.go:79] Authentication is disabled
I0716 17:25:32.347202       1 deprecated_insecure_serving.go:51] Serving healthz insecurely on [::]:10251
I0716 17:25:32.347934       1 secure_serving.go:123] Serving securely on [::]:10259

kubectl edit node mycluster-control-plane
failure-domain.beta.kubernetes.io/zone: "az-1"
kubectl edit node mycluster-worker
failure-domain.beta.kubernetes.io/zone: "az-2"
kubectl edit node mycluster-worker2
failure-domain.beta.kubernetes.io/zone: "az-3"

kubectl edit pv pvc-0
failure-domain.beta.kubernetes.io/zone: "az-1"
kubectl edit pv pvc-1
failure-domain.beta.kubernetes.io/zone: "az-2"
kubectl edit pv pvc-2
failure-domain.beta.kubernetes.io/zone: "az-3"


I0716 18:02:42.314784       1 plugin.go:64] Built Zonal Volume Distribution: map[string]map[uint]bool{"az-1":map[uint]bool{0x0:true}, "az-2":map[uint]bool{0x1:true}, "az-3":map[uint]bool{0x2:true}}
I0716 18:02:42.319796       1 plugin.go:106] Built Node List: []plugin.Node{plugin.Node{Name:"mycluster-worker2", Zone:"az-3"}, plugin.Node{Name:"mycluster-control-plane", Zone:"az-1"}, plugin.Node{Name:"mycluster-worker", Zone:"az-2"}}
I0716 18:02:42.319886       1 plugin.go:107] Built Ideal Zonal Topology: plugin.ZonalTopology{"az-1", "az-2", "az-3"}
I0716 18:02:42.319896       1 plugin.go:108] Ideal zone for ordinal 0 is az-1
I0716 18:02:42.319823       1 plugin.go:106] Built Node List: []plugin.Node{plugin.Node{Name:"mycluster-worker2", Zone:"az-3"}, plugin.Node{Name:"mycluster-control-plane", Zone:"az-1"}, plugin.Node{Name:"mycluster-worker", Zone:"az-2"}}
I0716 18:02:42.319909       1 plugin.go:107] Built Ideal Zonal Topology: plugin.ZonalTopology{"az-1", "az-2", "az-3"}
I0716 18:02:42.319914       1 plugin.go:108] Ideal zone for ordinal 0 is az-1
I0716 18:02:42.322270       1 plugin.go:106] Built Node List: []plugin.Node{plugin.Node{Name:"mycluster-worker2", Zone:"az-3"}, plugin.Node{Name:"mycluster-control-plane", Zone:"az-1"}, plugin.Node{Name:"mycluster-worker", Zone:"az-2"}}
I0716 18:02:42.322324       1 plugin.go:107] Built Ideal Zonal Topology: plugin.ZonalTopology{"az-1", "az-2", "az-3"}
I0716 18:02:42.322334       1 plugin.go:108] Ideal zone for ordinal 0 is az-1
I0716 18:02:48.470681       1 plugin.go:64] Built Zonal Volume Distribution: map[string]map[uint]bool{"az-1":map[uint]bool{0x0:true}, "az-2":map[uint]bool{0x1:true}, "az-3":map[uint]bool{0x2:true}}
I0716 18:02:48.470979       1 plugin.go:106] Built Node List: []plugin.Node{plugin.Node{Name:"mycluster-worker2", Zone:"az-3"}, plugin.Node{Name:"mycluster-control-plane", Zone:"az-1"}, plugin.Node{Name:"mycluster-worker", Zone:"az-2"}}
I0716 18:02:48.471061       1 plugin.go:107] Built Ideal Zonal Topology: plugin.ZonalTopology{"az-1", "az-2", "az-3"}
I0716 18:02:48.471077       1 plugin.go:108] Ideal zone for ordinal 1 is az-2
I0716 18:02:48.471098       1 plugin.go:106] Built Node List: []plugin.Node{plugin.Node{Name:"mycluster-worker2", Zone:"az-3"}, plugin.Node{Name:"mycluster-control-plane", Zone:"az-1"}, plugin.Node{Name:"mycluster-worker", Zone:"az-2"}}
I0716 18:02:48.470982       1 plugin.go:106] Built Node List: []plugin.Node{plugin.Node{Name:"mycluster-worker", Zone:"az-2"}, plugin.Node{Name:"mycluster-worker2", Zone:"az-3"}, plugin.Node{Name:"mycluster-control-plane", Zone:"az-1"}}
I0716 18:02:48.471187       1 plugin.go:107] Built Ideal Zonal Topology: plugin.ZonalTopology{"az-1", "az-2", "az-3"}
I0716 18:02:48.471196       1 plugin.go:108] Ideal zone for ordinal 1 is az-2
I0716 18:02:48.471176       1 plugin.go:107] Built Ideal Zonal Topology: plugin.ZonalTopology{"az-1", "az-2", "az-3"}
I0716 18:02:48.471203       1 plugin.go:108] Ideal zone for ordinal 1 is az-2
I0716 18:02:54.384485       1 plugin.go:64] Built Zonal Volume Distribution: map[string]map[uint]bool{"az-1":map[uint]bool{0x0:true}, "az-2":map[uint]bool{0x1:true}, "az-3":map[uint]bool{0x2:true}}
I0716 18:02:54.385100       1 plugin.go:106] Built Node List: []plugin.Node{plugin.Node{Name:"mycluster-worker2", Zone:"az-3"}, plugin.Node{Name:"mycluster-control-plane", Zone:"az-1"}, plugin.Node{Name:"mycluster-worker", Zone:"az-2"}}
I0716 18:02:54.385174       1 plugin.go:107] Built Ideal Zonal Topology: plugin.ZonalTopology{"az-1", "az-2", "az-3"}
I0716 18:02:54.385201       1 plugin.go:108] Ideal zone for ordinal 2 is az-3
I0716 18:02:54.385333       1 plugin.go:106] Built Node List: []plugin.Node{plugin.Node{Name:"mycluster-worker2", Zone:"az-3"}, plugin.Node{Name:"mycluster-control-plane", Zone:"az-1"}, plugin.Node{Name:"mycluster-worker", Zone:"az-2"}}
I0716 18:02:54.385376       1 plugin.go:107] Built Ideal Zonal Topology: plugin.ZonalTopology{"az-1", "az-2", "az-3"}
I0716 18:02:54.385401       1 plugin.go:108] Ideal zone for ordinal 2 is az-3
I0716 18:02:54.385481       1 plugin.go:106] Built Node List: []plugin.Node{plugin.Node{Name:"mycluster-worker2", Zone:"az-3"}, plugin.Node{Name:"mycluster-control-plane", Zone:"az-1"}, plugin.Node{Name:"mycluster-worker", Zone:"az-2"}}
I0716 18:02:54.385527       1 plugin.go:107] Built Ideal Zonal Topology: plugin.ZonalTopology{"az-1", "az-2", "az-3"}
I0716 18:02:54.385564       1 plugin.go:108] Ideal zone for ordinal 2 is az-3

root@DESKTOP-H1BKVCJ:~# kubectl get pods -o wide
NAME      READY   STATUS    RESTARTS   AGE   IP            NODE                      NOMINATED NODE   READINESS GATES
mongo-0   2/2     Running   0          82s   10.244.0.12   mycluster-control-plane   <none>           <none>
mongo-1   2/2     Running   0          76s   10.244.2.6    mycluster-worker          <none>           <none>
mongo-2   2/2     Running   0          70s   10.244.1.5    mycluster-worker2         <none>           <none>
```
