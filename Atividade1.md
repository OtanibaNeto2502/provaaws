## Autor : Otaniba Neto
| ![image](https://github.com/OtanibaNeto2502/provaaws/assets/139134335/8b9b0c3a-5d5b-40a6-8e83-a145b9eb0b6a) |
| :---: |
### Inicialização da maquina virtual linux com as configurações determinadas pelo aplicador da avaliação!
* Requisitos AWS:
* Gerar uma chave pública para acesso ao ambiente;
* Criar 1 instância EC2 com o sistema operacional Amazon Linux 2 (Famíliat3.small, 16 GB SSD);
* Gerar 1 elastic IP e anexar à instância EC2;
* Liberar as portas de comunicação para acesso público: (22/TCP, 111/TCP e UDP, 2049/TCP/UDP, 80/TCP, 443/TCP). 
### Codigo de inicialização da maquina virtual!
* Configuração da instância
``` js
{
  "MaxCount": 1,
  "MinCount": 1,
  "ImageId": "ami-04823729c75214919",
  "InstanceType": "t2.micro",
  "KeyName": "otanibanetonovavpc",
  "EbsOptimized": false,
  "BlockDeviceMappings": [
    {
      "DeviceName": "/dev/xvda",
      "Ebs": {
        "Encrypted": false,
        "DeleteOnTermination": true,
        "SnapshotId": "snap-02f54566c0793da5a",
        "VolumeSize": 16,
        "VolumeType": "gp2"
      }
    }
  ],
  "NetworkInterfaces": [
    {
      "SubnetId": "subnet-006fd4628a6a67ab6",
      "AssociatePublicIpAddress": true,
      "DeviceIndex": 0,
      "Groups": [
        "<groupId of the new security group created below>"
      ]
    }
  ],
  "TagSpecifications": [
    {
      "ResourceType": "instance",
      "Tags": [
        {
          "Key": "Name",
          "Value": "PB IFMT - UTFPR"
        },
        {
          "Key": "CostCenter",
          "Value": "C092000004"
        },
        {
          "Key": "Project",
          "Value": "PB IFMT - UTFPR"
        }
      ]
    },
    {
      "ResourceType": "volume",
      "Tags": [
        {
          "Key": "Name",
          "Value": "PB IFMT - UTFPR"
        },
        {
          "Key": "CostCenter",
          "Value": "C092000004"
        },
        {
          "Key": "Project",
          "Value": "PB IFMT - UTFPR"
        }
      ]
    },
    {
      "ResourceType": "network-interface",
      "Tags": [
        {
          "Key": "Name",
          "Value": "PB IFMT - UTFPR"
        },
        {
          "Key": "CostCenter",
          "Value": "C092000004"
        },
        {
          "Key": "Project",
          "Value": "PB IFMT - UTFPR"
        }
      ]
    }
  ],
  "PrivateDnsNameOptions": {
    "HostnameType": "ip-name",
    "EnableResourceNameDnsARecord": false,
    "EnableResourceNameDnsAAAARecord": false
  }
}
```
### Nova configuração do grupo de segurança
* Chamada de API: CreateSecurityGroup
``` js
{
  "GroupName": "otanibanovo",
  "Description": "launch-wizard-2 created 2023-07-12T13:44:45.311Z",
  "VpcId": "vpc-0968d4e2ef767ce28"
}
* Chamada de API: AuthorizeSecurityGroupIngress

{
  "GroupId": "<groupId of the security group created above>",
  "IpPermissions": [
    {
      "IpProtocol": "tcp",
      "FromPort": 22,
      "ToPort": 22,
      "IpRanges": [
        {
          "CidrIp": "0.0.0.0/0"
        }
      ],
      "Ipv6Ranges": [
        {
          "CidrIpv6": "::/0"
        }
      ]
    },
    {
      "IpProtocol": "tcp",
      "FromPort": 80,
      "ToPort": 80,
      "IpRanges": [
        {
          "CidrIp": "0.0.0.0/0"
        }
      ],
      "Ipv6Ranges": [
        {
          "CidrIpv6": "::/0"
        }
      ]
    },
    {
      "IpProtocol": "tcp",
      "FromPort": 443,
      "ToPort": 443,
      "IpRanges": [
        {
          "CidrIp": "0.0.0.0/0"
        }
      ],
      "Ipv6Ranges": [
        {
          "CidrIpv6": "::/0"
        }
      ]
    },
    {
      "IpProtocol": "tcp",
      "FromPort": 2049,
      "ToPort": 2049,
      "IpRanges": [
        {
          "CidrIp": "0.0.0.0/0"
        }
      ],
      "Ipv6Ranges": [
        {
          "CidrIpv6": "::/0"
        }
      ]
    },
    {
      "IpProtocol": "tcp",
      "FromPort": 111,
      "ToPort": 111,
      "IpRanges": [
        {
          "CidrIp": "0.0.0.0/0"
        }
      ],
      "Ipv6Ranges": [
        {
          "CidrIpv6": "::/0"
        }
      ]
    },
    {
      "IpProtocol": "udp",
      "FromPort": 111,
      "ToPort": 111
    }
  ]
}
```
### Configuração de rede.
![image](https://github.com/OtanibaNeto2502/prova_linux/assets/139134335/855c0377-6ff9-448b-bc20-372e0a821337)

### Criação do grupo de segurança com o intuito de liberar as portas de comunicação para acesso público: (22/TCP,111/TCP e UDP, 2049/TCP/UDP, 80/TCP, 443/TCP).
![image](https://github.com/OtanibaNeto2502/prova_linux/assets/139134335/f606d79d-6d8b-43e7-8a0f-e5fe10ffd7a7)
![image](https://github.com/OtanibaNeto2502/prova_linux/assets/139134335/c1173fc1-f117-4e1f-8a05-57577f04fc44)

### Configuração de armazenameto.
![image](https://github.com/OtanibaNeto2502/prova_linux/assets/139134335/6d59d871-87c9-4d0d-bef7-d9b12d72d0d7)

### Primeiro Acesso via console AWS.
![image](https://github.com/OtanibaNeto2502/prova_linux/assets/139134335/3f5e9336-21d2-49ec-a107-7137e91249e2)

### Criando EFS.
![image](https://github.com/OtanibaNeto2502/prova_linux/assets/139134335/66d55988-9bc5-414b-995c-ad1b1c956c62)
### Alterando security grup do EFS.
![image](https://github.com/OtanibaNeto2502/prova_linux/assets/139134335/afa5e930-cab1-4972-8c7b-686b03c7e5da)
### Anexando EFS a instancia!
![image](https://github.com/OtanibaNeto2502/prova_linux/assets/139134335/63033f41-8975-4a64-8b44-d5d81b86c701)
### Criando pasta com o nome otanibaneto dentro do EFS.
![image](https://github.com/OtanibaNeto2502/prova_linux/assets/139134335/fcc772d9-c25f-4d21-98be-47c6a4178014)
### Criando servidor APACHE.
Comandos ultilizados:
    
``` bash
yum install httpd

systemctl start httpd

systemctl enable httpd
```
### Verificando se o servidor esta online:
![image](https://github.com/OtanibaNeto2502/prova_linux/assets/139134335/752e1178-de1b-4edc-9624-3afb7d6a6767)
### Script para verificação do servidor APACHE
![image](https://github.com/OtanibaNeto2502/prova_linux/assets/139134335/eaefde30-3519-442e-b6d8-1ca193529ab1)
### Script para automação do processo de salvamento de log.
![image](https://github.com/OtanibaNeto2502/prova_linux/assets/139134335/9c669d2d-fa22-4167-94a0-2e7c22d95592)   
### Acessando arquivo de Log.
![image](https://github.com/OtanibaNeto2502/prova_linux/assets/139134335/474563f4-7f16-451d-9c0c-c3c78fb5d495)
### Arquivo de log.
![image](https://github.com/OtanibaNeto2502/prova_linux/assets/139134335/cbf65cf8-dd38-4a50-8b98-10ca682385db)



