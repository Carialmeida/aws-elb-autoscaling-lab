# ☁️ Scaling and Load Balancing Your Architecture — AWS Lab

> **Projeto prático AWS:** Implementando Elastic Load Balancing (ELB) e Auto Scaling para garantir alta disponibilidade e escalabilidade automática de aplicações web.  
> ⏱️ Duração: aproximadamente **45 minutos**

---

## 🧩 Visão Geral

Neste laboratório, configurei um ambiente **resiliente e escalável** usando:
- **Elastic Load Balancer (ELB)** para distribuir tráfego entre instâncias EC2  
- **Auto Scaling Group (ASG)** para ajustar automaticamente a capacidade conforme a demanda  
- **CloudWatch** para monitoramento e alarmes automáticos

---

## ⚙️ Arquitetura

### **Arquitetura final**

```mermaid
graph TD
    Client((Usuário)) --> |HTTP| ALB[Application Load Balancer]
    subgraph VPC["Lab VPC"]
        subgraph Public_Subnets["Subnets Públicas"]
            ALB
        end
        subgraph Private_Subnets["Subnets Privadas"]
            EC2a[EC2 Instance - AZ1]
            EC2b[EC2 Instance - AZ2]
        end
    end
    ALB --> EC2a
    ALB --> EC2b
    EC2a --> |Métrica CPU| CW[CloudWatch]
    EC2b --> |Métrica CPU| CW
    CW --> ASG[Auto Scaling Group]
    ASG --> |Cria / Remove instâncias| EC2a
    ASG --> EC2b

    style Client fill:#d3f9d8,stroke:#228b22,stroke-width:1px
    style ALB fill:#f3f9ff,stroke:#0073bb,stroke-width:1px
    style EC2a fill:#fff3cd,stroke:#f0ad4e,stroke-width:1px
    style EC2b fill:#fff3cd,stroke:#f0ad4e,stroke-width:1px
    style CW fill:#e8f5e9,stroke:#388e3c,stroke-width:1px
    style ASG fill:#fde2e4,stroke:#c62828,stroke-width:1px
