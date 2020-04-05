# Desafio Itau - Stack IaC

Este projeto entrega um ambiente inspirado no Well-Architected Framework da AWS.

## Getting Started

O YML do CloudFormation, através de Metadata e Parameters, já orienta o usuário acerca das variáveis necessárias para este piloto.

Um relatório técnico neste repo descreve mais profundamente o que a stack irá produzir.

### Prerequisites

Você precisa de apenas duas coisas para rodar a stack:

1. Key-Pair previamente criado. Será utilizado nas Bastions e também na Ec2 Fleet (caso você queria acessar para eventuais TS).

2. OAuth Token do GitHub. Para o teste iremos utilizar um Token simples de leitura.

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
