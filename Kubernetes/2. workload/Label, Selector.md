1. Label
- 새로운 레이블 추가
``` bash
kubectl label pod http-go-v2 test=foo
```
<br>

- 기존의 레이블을 수정 
``` bash
kubectl label pod http-go-v2 rel=beta --overwwrite
```
<br>

- 레이블 삭제
``` bash
kubectl label pod http-go-v2 rel-
```
<br>

- 전체 레이블 보기
``` bash
kubectl get pod --show-labels
```
<br>

- 특정 레이블 컬럼으로 확인
``` bash
kubectl get pod -L app,rel
```
<br>

레이블 필터링
- 레이블이 env 인것 검색
``` bash
kubectl get pod --show-labels -l 'env'
```
<br>

- 레이블이 env 가 아닌것 검색
``` bash
kubectl get pod --show-labels -l 'env'
```
<br>

- 레이블 env 값이 test인것 검색
``` bash
kubectl get pod --show-labels -l 'env!=test'
```
<br>

- 레이블 env 값이 test가 아니고 rel이 beta인것 검색
``` bash
kubectl get pod --show-labels -l 'env!=test,rel=beta'
```
<br>

