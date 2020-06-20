# Sacc4 - cli example helper

Instantiate the chaincode
```bash 
peer chaincode instantiate -n sacc4 -v 1.0 -o orderer.morgen.net:7050 -C channel1  -c '{"Args":["msg","hello blockchain"]}' --tls --cafile /tmp/hyperledger/mars.morgen.net/peers/peer0/tls-msp/tlscacerts/tls-ca-tls-morgen-net-7052.pem
```

Query the instantiated key
```bash
peer chaincode query -n sacc4 -c '{"Args":["query","msg"]}' -C channel1 --tls --cafile /tmp/hyperledger/mars.morgen.net/peers/peer0/tls-msp/tlscacerts/tls-ca-tls-morgen-net-7052.pem
```

Set a new value to the key
```bash 
peer chaincode invoke -n sacc4 -c '{"Args":["set", "msg","hello morgen.net history 1"]}' -C channel1  --tls --cafile /tmp/hyperledger/mars.morgen.net/peers/peer0/tls-msp/tlscacerts/tls-ca-tls-morgen-net-7052.pem
```

Get the history of this value
```bash
peer chaincode invoke -n sacc4 -c '{"Args":["history", "msg"]}' -C channel1  --tls --cafile /tmp/hyperledger/mars.morgen.net/peers/peer0/tls-msp/tlscacerts/tls-ca-tls-morgen-net-7052.pem
```

Query the value of this key
```bash
peer chaincode query -n sacc4 -c '{"Args":["query","msg"]}' -C channel1 --tls --cafile /tmp/hyperledger/mars.morgen.net/peers/peer1/tls-msp/tlscacerts/tls-ca-tls-morgen-net-7052.pem
```

Get all keys
```bash
peer chaincode query -n sacc4 -c '{"Args":["all"]}' -C channel1 --tls --cafile /tmp/hyperledger/mars.morgen.net/peers/peer1/tls-msp/tlscacerts/tls-ca-tls-morgen-net-7052.pem
```