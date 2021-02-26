# DDD : 도메인 주도 설계

- 느슨한 결합 ( loose coupling )
- 높은 응집도 ( high cohesion )



도메인 모델 설게시 요구 되는 3가지

1. 모델과 핵심 설계는 상호 영향을 주고 받으며 구체화 된다.
2. 모델은 모든 팀 구성원들이 사용하는 언어의 근간을 이룬다.
3. 모델은 불순물을 걸러낸 핵심 지식만을 포함한다.



DDD란?

도메인 중심으로 생각한 설계 방법

도메인 : 소프트웨어가 취급하는 어떤 활동이나 관심과 관계가 있는 지식



1. 시나리오로부터 모델을 만들어낸다.

2. DDD에는 model exploration whirlpool 이라는 모델을 정제하기 위한 프로세스 정의

   ![img](C:\Users\Nomad\Desktop\TIL\img\model_exploration_cycle_v2010-06-19.png)



## 유비쿼터스 언어 (Ubiquitous Language / 보편언어)

팀 내의 의사소통 및 구현까지 연결할 수 있도록 하고 있음. 사용되는 언어에 대한 이해가 서로 일치해야하며, 그렇지 않은 경우, 모델 변경 및 고드상으로는 Refacotoring으로 이어지는 과정이 나타난다.

