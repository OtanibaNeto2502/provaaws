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
![image](https://github.com/OtanibaNeto2502/provaaws/blob/main/imagens/1.png)

### Criação do grupo de segurança com o intuito de liberar as portas de comunicação para acesso público: (22/TCP,111/TCP e UDP, 2049/TCP/UDP, 80/TCP, 443/TCP).
![image](https://github.com/OtanibaNeto2502/provaaws/blob/main/imagens/2.png)
![image](https://github.com/OtanibaNeto2502/provaaws/blob/main/imagens/3.png)

### Configuração de armazenameto.
![image](https://github.com/OtanibaNeto2502/provaaws/blob/main/imagens/4.png)

### Primeiro Acesso via console AWS.
![image](https://github.com/OtanibaNeto2502/provaaws/blob/main/imagens/5.png)

### Criando EFS.
![image](https://github.com/OtanibaNeto2502/provaaws/blob/main/imagens/6.png)
### Alterando security grup do EFS.
![image](https://github.com/OtanibaNeto2502/provaaws/blob/main/imagens/7.png)
### Anexando EFS a instancia!
![image](https://github.com/OtanibaNeto2502/provaaws/blob/main/imagens/8.png)
### Criando pasta com o nome otanibaneto dentro do EFS.
![image](https://github.com/OtanibaNeto2502/provaaws/blob/main/imagens/9.png)
### Criando servidor APACHE.
Comandos ultilizados:
    
``` bash
yum install httpd

systemctl start httpd

systemctl enable httpd
```
### Verificando se o servidor esta online:
![image](https://github.com/OtanibaNeto2502/provaaws/blob/main/imagens/10.png)
### Script para verificação do servidor APACHE
![image](https://github.com/OtanibaNeto2502/provaaws/blob/main/imagens/11.png)
### Script para automação do processo de salvamento de log.
![image](https://github.com/OtanibaNeto2502/provaaws/blob/main/imagens/12.png)
### Acessando arquivo de Log.
![image](https://github.com/OtanibaNeto2502/provaaws/blob/main/imagens/13.png)
### Arquivo de log.
![image](https://github.com/OtanibaNeto2502/provaaws/blob/main/imagens/14.png)


