# fabric

## Smart Contract
./contract/donation/donation.go -> 디앱에서 제공하는 기본적인 스마트 컨트랙트가 담겨있음
./contract/donation/mymarbles   -> 프라이빗 데이터를 담는곳


## Start Hyperledger Fabric
```bash
cd /donation/network
./generate.sh
./start.sh
./cc_donation.sh
```

네트워크 삭제
```bash
cd /donation/network
./teardown.sh
```