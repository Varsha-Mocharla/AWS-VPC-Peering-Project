Main communication flow
1. Administrator connects to the Bastion Host through SSH.
2. Bastion Host provides controlled SSH access to App-A and App-B.
3. VPC Peering connects VPC A and VPC B.
4. Route tables direct traffic to the peer VPC.
5. App-A and App-B communicate through private IP addresses using ICMP.

6. 
flowchart LR
    U["Administrator"]
    NET["Internet"]
    IGW["Internet Gateway"]

    subgraph VA["VPC A — 10.10.0.0/16"]
        direction TB
        subgraph PUB["Public Subnet — 10.10.1.0/24"]
            B["Bastion Host<br/>10.10.1.10<br/>Public IP: 54.252.166.57"]
        end
        subgraph PA["Private Subnet — 10.10.2.0/24"]
            A["App-A EC2<br/>10.10.2.10"]
        end
        RTA["Route Table<br/>10.20.0.0/16 → Peering"]
    end

    PCX["VPC Peering Connection<br/>ACTIVE"]

    subgraph VB["VPC B — 10.20.0.0/16"]
        direction TB
        subgraph PB["Private Subnet — 10.20.1.0/24"]
            C["App-B EC2<br/>10.20.1.10"]
        end
        RTB["Route Table<br/>10.10.0.0/16 → Peering"]
    end

    U -->|SSH| NET
    NET --> IGW
    IGW --> B
    B -->|Private SSH| A
    B -->|Private SSH via Peering| C
    RTA --- PCX
    PCX --- RTB
    A <-->|Bidirectional ICMP / Ping| PCX
    PCX <-->|Bidirectional ICMP / Ping| C

    classDef public fill:#dbeafe,stroke:#2563eb,color:#1e3a8a
    classDef private fill:#dcfce7,stroke:#16a34a,color:#14532d
    classDef network fill:#fef3c7,stroke:#d97706,color:#78350f
    class B public
    class A,C private
    class PCX,IGW network
<img width="4640" height="594" alt="mermaid-diagram" src="https://github.com/user-attachments/assets/f18d05b7-3bc1-44f6-a65a-992e5e391285" />
<img width="4640" height="594" alt="mermaid-diagram" src="https://github.com/user-attachments/assets/275cc2d7-386a-4276-9a65-cca1e3f31d2b" />
