# fabric

## Smart Contract
./contract/donation/donation.go -> 디앱에서 제공하는 기본적인 스마트 컨트랙트가 담겨있음  

- 각각은 다른 예제지만 어차피 "github.com/hyperledger/fabric/core/chaincode/shim" 이놈이 모든 API를 컨트롤 하기 때문에 
marbles 예제를 그대로 가져와도 동작한다.  
  
- cc_donation.sh 안에서 체인코드를 설치할 때, docker exec cli peer chaincode install -n donation -v 1.0 -p github.com/donation  
설치하는 경로가 github.com/donation 으로 돼있어서 ./contract/donation 안에 있는 모든 체인 코드 소스파일들이 설치된다.  
따라서 여러 소스파일로 체인코드를 관리할 수 있다.  
  
-> ./network/docker-compose.yml 안에 cli 선언부분(맨 밑)을 보면  
    volumes:  
        - /var/run/:/host/var/run/  
        - ./../contract/:/opt/gopath/src/github.com/  
        - ./crypto-config:/etc/hyperledger/crypto  
        - ./config:/etc/hyperledger/configtx  
이것이 있는데, 이중에 - ./../contract/:/opt/gopath/src/github.com/ 요놈이 ./contract 파일 안에있는 소스들을 도커 컨테이너와 공유해서  
체인 코드를 설치할 때 설치가 되는 것이다.

* 한줄 요약 -> ./network/docker-compose.yml 에 자기가 체인코드를 설치할 파일 주소를 적고 그 파일 안에  
자기가 설치하고 싶은 체인 코드 소스파일들을 넣으면 된다 ** 

## Start Hyperledger Fabric
```bash
cd /donation/network
./generate.sh
./start.sh
./cc_donation.sh

or 

./po.sh
```

네트워크 삭제
```bash
cd /donation/network
./teardown.sh
```

## Start WebServer
```bash
cd /donation/prototype
rm -rf wallet
node enrollAdmin
node registerUser
node server

or

./startServer.sh
```