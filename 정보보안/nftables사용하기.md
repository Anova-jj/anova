
# netfilter
nftables를 이해하기 위해서는 netfilter라는 커널 프레임워크 부터 이해해야한다.
리눅스 커널에서는 네트워크 패킷의 라우팅 시, 특정 point마다 패킷을 hooking하여 특정 동작을 수행하도록 할 수 있다.

이러한 point들을 hooking point 라고 하고, 이러한 hooking point에서 패킷을 가로채 호스트로 패킷을 accept할지, drop/rejet할지 결정할 수 있다.

이러한 패킷 필터링 기능은 netfilter 프레임 워크에서 지원해주는 기능이며,
iptables와 nftables 같은 유틸리티가 netfilter를 조작하도록 도와주는 패키지다.





# arch linux에서 nftables 설치하기

```
sudo pacman -S nftables
```
그냥 팩맨으로 쉽게 설치가 가능하다.


# iptables와의 비교

리눅스 상태기반 방화벽인 iptables와 동일하게 netfilter을 사용한다.

그러나 iptables와 차이가 있다면 iptables는 predefined된 테이블을 제공하지만 nftables는 좀더 섬세하게 설정을 적용할 수 있도록 기능을 제공하는 것으로 보인다. ~~아님말고 나중에 제대로 확인해보겠다.~~


# nft 설정파일의 기본 구조

Table
├─Chain1
│ ├─Rule1a
│ └─Rule1b
├─Chain2
│ ├─Rule2a
│ ├─Rule2b
│ └─Rule2c
└─Chain3
  └─Rule3a


## Tables
iptables의 테이블은 filter,nat, mangle 등 미리 정의된 테이블이 있는 반면에
nftables는 미리 정의된 테이블이 존재하지 않는다!!

테이블의 기본 구조는 다음과 같다.

1. tables기본 구조
> \[address family] \[name]

2. address family 종류
1) ip
2) ip6
3) inet
4) arp

## Chains 및 Hooks


