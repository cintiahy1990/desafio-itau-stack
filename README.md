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

  1-) A stack vai criar uma VPC, com duas subnets publicas e duas subnets privadas, distribuidas
  em duas AZ's.
  2-) Pra tornar as duas primeiras subnets publicas, a stack vai entregar um IGW. Este, apenas
  atrelado na Routing Table Publica.
  3-) Para o egress, vamos utilizar um NAT GW em cada subnet publica. Assim nao temos um unico ponto de falha.
  3.1-) Cada Routing Table das subnets privadas vai ter o destination 0.0.0.0/0 pro seu respectivo nat-gw (tem dois)
  4-) Vamos criar uma pequena Bastion em cada subnet publica, para permitir o acesso SSH e, a partir deste,
  poder cair em alguma outra EC2 em subnets privadas. ~~IMPORTANTE~~ Aqui sera necessario um key-pair.
  5-) Criaremos um VPC Endpoint (GW) para o servico do S3, ja que nao queremos acessar os buckets pela internet.
  ---- IMPORTANTE - Explicacao continua no GitHub


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
