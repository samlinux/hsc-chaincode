# Additional Presentation Material 

Start the first panel session.
```bash 
# start the session and the first panel
tmux new -s fabric

# switch to the chaincode-docker-devmode folder
cd fabric-samples/chaincode-docker-devmode

# start the dev network
docker-compose -f docker-compose-simple.yaml up
```

Start the second panel session.
```bash 
# create a new panel
CTRL + b \" (one double quote)

# switch to the chaincode-docker-devmode folder
cd fabric-samples/chaincode-docker-devmode

# switch into the chaincode container/folder
docker exec -it chaincode bash

# switch into the chaincode folder
cd nfdt01

# build the chaincode
go build

# run the chaincode
CORE_PEER_ADDRESS=peer:7052 CORE_CHAINCODE_ID_NAME=mycc:0 ./nfdt01
```

Start the third panel session.
```bash
# switch into the chaincode container/folder
docker exec -it cli bash
cd /opt/gopath/src

# Install and instantiate the chaincode
peer chaincode install -p chaincodedev/chaincode/nfdt01 -n mycc -v 0
peer chaincode instantiate -n mycc -v 0 -c '{"Args":[]}' -C myc

# Invoke the chaincode
peer chaincode invoke -n mycc -c '{"Args":["add","art","Art 1","this could be long","rbole","2020-07-15T15:04:05.000Z"]}' -C myc

# Query the chaincode

peer chaincode query -n mycc -c '{"Args":["add","art","Art 10","this could be long","rbole","2020-07-15T15:04:05.000Z"]}' -C myc

peer chaincode invoke -n mycc -c '{"Args":["add","art","Art 2","Fabric v2.0 introduces decentralized governance for smart contracts, with a new process for installing a chaincode on your peers and starting it on a channel. The new Fabric chaincode lifecycle allows multiple organizations to come to agreement on the parameters of a chaincode, such as the chaincode endorsement policy, before it can be used to interact with the ledger. The new model offers several improvements over the previous lifecycle:","snorre","2020-07-13T15:10:05.000Z"]}' -C myc

peer chaincode invoke -n mycc -c '{"Args":["add","art","Art 3","Before installing and instantiating the marbles chaincode, we need to start up the BYFN network. For the sake of this tutorial, we want to operate from a known initial state. The following command will kill any active or stale docker containers and remove previously generated artifacts. Therefore let’s run the following command to clean up any previous environments:","rbole","2020-07-10T15:04:05.000Z"]}' -C myc

peer chaincode invoke -n mycc -c '{"Args":["add","art","Art 3","Before installing and instantiating the marbles chaincode, we need to start up the BYFN network. For the sake of this tutorial, we want to operate from a known initial state. The following command will kill any active or stale docker containers and remove previously generated artifacts. Therefore let’s run the following command to clean up any previous environments:","snorre","2020-07-20T15:04:05.000Z"]}' -C myc

peer chaincode query -n mycc -c '{"Args":["queryById","5296f881-50ac-46b5-b4b3-ea7bd2c0df03"]}' -C myc |jq '.'

peer chaincode query -n mycc -c '{"Args":["queryByOwner","rbole"]}' -C myc |jq '.'

peer chaincode query -n mycc -c '{"Args":["queryAdHoc","{\"selector\": {\"name\": \"Art 1\"}}"]}' -C myc |jq '.'

peer chaincode query -n mycc -c '{"Args":["queryAdHoc","{\"selector\": {\"_id\": {\"$gt\":\"\"}}}"]}' -C myc |jq '.'

peer chaincode query -n mycc -c '{"Args":["queryAdHoc","{\"selector\": {\"owner\": \"rbole\"}, \"use_index\":[\"_design/indexOwnerDoc\", \"indexOwner\"]}"]}' -C myc |jq '.'

peer chaincode query -n mycc -c '{"Args":["queryAdHoc","{\"selector\": {\"time\": {\"$gt\":\"2020-07-16\"}}}, \"use_index\":[\"_design/indexTimeDoc\", \"indexTime\"]"]}' -C myc |jq '.'
```

Helper to escape the json query string
```bash
# escape for fabric
jq -aRs . <<< '{"selector": {"owner": "rbole"}, "use_index":["_design/indexOwnerDoc", "indexOwner"]}'

# result 
"{\"selector\": {\"owner\": \"rbole\"}, \"use_index\":[\"_design/indexOwnerDoc\", \"indexOwner\"]}"
```