#Link for article
https://medium.com/@kctheservant/demo-of-three-node-two-channel-setup-in-hyperledger-fabric-54ba8a9c461f


ssh -i "kp1.pem" ubuntu@ec2-3-22-171-189.us-east-2.compute.amazonaws.com


#orderer
scp -i ~/Downloads/kp1.pem 3node2channel.tar ubuntu@ec2-18-221-26-62.us-east-2.compute.amazonaws.com:/home/ubuntu/fabric-samples/

#org1
scp -i ~/Downloads/kp1.pem 3node2channel.tar ubuntu@ec2-3-22-171-189.us-east-2.compute.amazonaws.com:/home/ubuntu/fabric-samples/

#org2
scp -i ~/Downloads/kp1.pem 3node2channel.tar ubuntu@ec2-18-191-117-71.us-east-2.compute.amazonaws.com:/home/ubuntu/fabric-samples/

#org3
scp -i ~/Downloads/kp1.pem 3node2channel.tar ubuntu@ec2-18-188-122-198.us-east-2.compute.amazonaws.com:/home/ubuntu/fabric-samples/


#orderer
ssh -i "kp1.pem" ubuntu@ec2-18-221-26-62.us-east-2.compute.amazonaws.com

#org1
ssh -i "kp1.pem" ubuntu@ec2-3-22-171-189.us-east-2.compute.amazonaws.com

#org2
ssh -i "kp1.pem" ubuntu@ec2-18-191-117-71.us-east-2.compute.amazonaws.com

#org3
ssh -i "kp1.pem" ubuntu@ec2-18-188-122-198.us-east-2.compute.amazonaws.com



tar xf 3node2channel.tar

cd 3node2channel/deployment


docker-compose -f docker-compose-orderer.yml up -d

docker-compose -f docker-compose-node1.yml up -d

docker-compose -f docker-compose-node2.yml up -d

docker-compose -f docker-compose-node3.yml up -d


docker exec -e "CORE_PEER_MSPCONFIGPATH=/var/hyperledger/users/Admin@org1.example.com/msp" peer0.org1.example.com peer channel create -o orderer.example.com:7050 -c channelall -f /var/hyperledger/configs/channelall.tx



IPs


Public

orderer- 18.221.26.62
org1- 3.22.171.189
org2- 18.191.117.71
org3- 18.188.122.198


private- 

orderer- 172.31.36.250
org1- 172.31.33.121
org2- 172.31.43.88
org3- 172.31.46.241

172.31.36.250 orderer.example.com
172.31.33.121 peer0.org2.example.com
172.31.43.88 peer0.org2.example.com
172.31.46.241 peer0.org2.example.com


sudo nano /etc/hosts