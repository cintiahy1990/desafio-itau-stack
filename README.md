# Desafio Itau - Stack IaC

Este projeto entrega um ambiente inspirado no Well-Architected Framework da AWS.

## Getting Started

O YML do CloudFormation, através de Metadata e Parameters, já orienta o usuário acerca das variáveis necessárias para este piloto.

Um relatório técnico neste repo descreve mais profundamente o que a stack irá produzir.

### Prerequisites

Você precisa de apenas duas coisas para rodar a stack:

1. Key-Pair previamente criado. Será utilizado nas Bastions e também na Ec2 Fleet (caso você queria acessar para eventuais TS).

2. OAuth Token do GitHub. Para o teste iremos utilizar um Token simples de leitura.

### IaC - CloudFormation Description

Este template foi puramente insipirado no Well-Architected Framework da AWS, visando suprir as necessidades do projeto-desafio para o Itau Unibanco.

Segue abaixo uma descrição detalhada do que a stack está fazendo para este piloto:

  1-) A stack vai criar uma VPC, com duas subnets públicas e duas subnets privadas, distríbuidas
  em duas AZ's.

  2-) Pra tornar as duas primeiras subnets publicas, a stack vai entregar um IGW. Este, apenas
  atrelado na Routing Table Pública.

  3-) Para o egress, vamos utilizar um NAT GW em cada subnet pública. Assim nao temos um unico ponto de falha.

  3.1-) Cada Routing Table das subnets privadas vai ter o destination 0.0.0.0/0 pro seu respectivo nat-gw (tem dois)

  4-) Vamos criar uma pequena Bastion em cada subnet publica, para permitir o acesso SSH e, a partir deste,
  poder cair em alguma outra EC2 em subnets privadas. ~~IMPORTANTE~~ Aqui sera necessario um key-pair.

  5-) Criaremos um VPC Endpoint (GW) para o servico do S3, ja que nao queremos acessar os buckets pela internet.

  6-) Começa o processo de criação da EC2 Fleet que irá suportar a Aplicação.

  6.1-) Cria as IAM Roles necessárias para a EC2 interagir com o CodeDeploy

  6.2-) Cria a EC2 Fleet passando por um processo de Metadata e Userdata, instalando o Agente do CodeDeploy em cada EC2

  6.3-) Expõe, através de SG's, a SSH e a HTTP apenas para o CIDR da VPC. Aqui podemos usar o SG do ALB também.

  7-) Criação do CodeDeploy e sua respectiva Role com a Policy "AWSCodeDeployRole"

  7.1-) Criação de uma Application para suportar nossa App de Demo

  7.2-) Criação do Deployment Group com as configurações IN-PLACE utilizando um TAG Filter simples para encontrar a EC2-Fleet.

  8-) Criação do Bucket S3 para guardar os artefatos do Deploy em si. Ex: código fonte (não tenho processo de build)

  9-) Criação do WebHook que conectará o Repo do GitHub com o CodePipeline

  10-) Criação da Pipeline através do CodePipeline
  
  10.1-) A Pipeline possui dois stages: Source e o Deploy (batizado de Beta)

  10.2-) O Pipeline irá guardar os artefatos no Bucket S3 previamente criado.

  11-) Criação do ALB exposto (internet facing)

  11.2-) Este ALB irá escutar na porta 80 e encaminhará para a EC2 Fleet nas subnets privadas. 

## Built With

* [CloudFormation](https://aws.amazon.com/cloudformation/) - The IaC Engine


## Authors

* **Cintia Yamaki** - *Initial work* - [Cyaa](https://github.com/cintiahy1990)

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* Hat tip to anyone whose code was used
* Inspiration
* etc
