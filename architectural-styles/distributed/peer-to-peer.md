# Peer to Peer

**Peer-to-Peer (P2P) Architecture** is a decentralized network design where each participant (peer) has equivalent capabilities and responsibilities. Unlike client-server architecture, P2P networks do not have dedicated servers or clients; instead, each node can act as both a client and a server.

# Key Characteristics of Peer-to-Peer Architecture

1. Decentralization: P2P networks do not rely on a central server. Each peer can directly communicate with other peers, making the network more resilient to failures and distributing the load evenly.

2. Scalability: P2P networks can scale easily as new peers join, each contributing resources and capacity to the network.

3. Resource Sharing: Peers share resources (such as files, processing power, or bandwidth) directly with each other.

4. Equal Roles: All nodes in the network have equal roles and responsibilities, unlike client-server models where the server has a dominant role.

5. Dynamic Topology: The network topology can change dynamically as peers join or leave the network, making it adaptable and robust.

# Benefits of Peer-to-Peer Architecture

1. Reliability: The absence of a central server means there is no single point of failure, making the network more reliable.

2. Scalability: P2P networks can grow indefinitely as new peers join and share their resources.

3. Cost Efficiency: Resources are shared among peers, reducing the need for expensive centralized infrastructure.

4. Resource Utilization: Efficient use of available resources as each peer contributes to the network.

# Example in TypeScript

To illustrate Peer-to-Peer Architecture in TypeScript, let's consider a simple P2P file-sharing system using WebRTC for peer-to-peer communication.

**Basic Peer-to-Peer Connection Using WebRTC**

```typescript
// Peer A
const peerA = new RTCPeerConnection();
const dataChannelA = peerA.createDataChannel("fileTransfer");

dataChannelA.onopen = () => {
  console.log("Data channel is open");
  dataChannelA.send("Hello from Peer A");
};

dataChannelA.onmessage = (event) => {
  console.log("Received message from Peer B:", event.data);
};

peerA.onicecandidate = (event) => {
  if (event.candidate) {
    // Send candidate to Peer B
  }
};

// Create and send offer to Peer B
peerA.createOffer().then((offer) => {
  peerA.setLocalDescription(offer);
  // Send offer to Peer B
});

// Peer B
const peerB = new RTCPeerConnection();

peerB.ondatachannel = (event) => {
  const dataChannelB = event.channel;
  dataChannelB.onopen = () => {
    console.log("Data channel is open");
  };

  dataChannelB.onmessage = (event) => {
    console.log("Received message from Peer A:", event.data);
    dataChannelB.send("Hello from Peer B");
  };
};

peerB.onicecandidate = (event) => {
  if (event.candidate) {
    // Send candidate to Peer A
  }
};

// Receive offer from Peer A and create answer
peerB.setRemoteDescription(offerFromPeerA).then(() => {
  peerB.createAnswer().then((answer) => {
    peerB.setLocalDescription(answer);
    // Send answer to Peer A
  });
});

// Peer A receives answer from Peer B
peerA.setRemoteDescription(answerFromPeerB);
```

In this example, two peers (Peer A and Peer B) establish a direct connection using WebRTC. They create a data channel for transferring messages. Peer A initiates the connection by creating an offer and sending it to Peer B. Peer B responds with an answer, and both peers exchange ICE candidates to establish a direct connection.

# Real-Life Analogy

**Neighborhood Library**: Imagine a neighborhood where residents share books directly with each other instead of borrowing them from a central library. Each resident (peer) can lend and borrow books (resources) from others. This system is decentralized, and each resident has equal responsibility and capability to share books.

# Summary

Peer-to-Peer Architecture is a powerful design pattern that promotes decentralization, scalability, and efficient resource utilization. By allowing each node to act as both client and server, P2P networks can adapt dynamically, distribute load evenly, and remain robust against failures. This architecture is commonly used in applications like file sharing, blockchain, and real-time communication systems.
