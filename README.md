# Documentação de Requisitos
*Membros:* 
* Leonardo Vinicius Galvão da Silva.

## Introdução
Este é um projeto extensionista para o curso de Análise e Desenvolvimento de Sistemas na faculdade PUC de Goiás.

O projeto consiste no desenvolvimento do levantamento de requisitos para um software real, compreendendo as fases de *levantamento de requisitos*, *prototipação*, *apresentação e entrega do projeto*.

## Objetivo Geral do Documento
Este documento tem informações dos requisitos iniciais para concepção de um Sistema de
Gerenciamento e Automatização de mensagens no atendimento ao cliente, utilizando a
API oficial da META.

## Objetivo Geral do Projeto
* Compreender a importância do levantamento de requisitos no ciclo de desenvolvimento de software.
* Aplicar técnicas de elicitação de requisitos para definir funcionalidades de um sistema cliente servidor.
* Utilizar ferramentas para prototipação.
* Trabalhar de forma colaborativa no desenvolvimento do projeto.

## Metodologia utilizada no projeto
* Fase 1 - Levantamento de Requisitos.
    * Aplicação da técnica de *entrevista* para o levantamento dos requisitos.
    * Documentação dos requisitos através do diagrama de uso.
* Fase 2 - Prototipação.
    * Utilização do Figma para a cosntrução do protótipo do sistema.
* Fase 3 - Apresentação e Entrega do Projeto.
    * Documentação final do projeto.
    * Apresentação do sistema desenvolvido (protótipo).

## Propósito Geral do Sistema
* Agilizar o atendimento ao cliente, através de um bot que realizará o atendimento
inicial aos clientes.
* Automatizar as conversas através de mensagens pré-definidas.
* Fornecer um número de Whatsapp que não será bloqueado pela Meta.
* Aumentar as vendas e diminuir a perda por falta ou demora no atendimento.

## Informações do Cliente
O nome do cliente é anônimo, sendo me permitido apenas a identificação do desenvolvedor senior que me acompanhou durante toda a etapa de levantamento de requisitos, que foi quem participou da entrevista respondendo às minhas perguntas.

* *Responsável:* Arthur Freitas.
* *Função:* engenheiro de software senior.
* *Assinatura:* 

## Requisitos do sistema

* O administrador terá um sistema web para acompanhar o dashboard contendo relatório sobre os atendimentos por departamento (quantidade de mensagens por departamento, por atendente, total), com período à escolha do administrador (horas, dias, meses), as métricas são a quantidade de atendimento por atendente e departamento, tempo de resposta entre as mensagens e tempo desde o inicio do atendimento até o seu encerramento.
* O sistem web deverá permitir o cadastro e exclusão de departamentos e atendentes por parte do administrador.
* O sistema web deverá fornecer ao administrador a opção de monitorar (ver) as conversas de todos os atendentes.
* O sistema web deverá permitir que o administrador possa configurar o chatbot (editar mensagens padrão do menú, criar e excluir mensagens automáticas).
* Os atendentes terão um aplicativo mobile com a mesma interface gráfica do aplicativo oficial do Whatsapp.
* O aplicativo mobile deverá conter as funções de ler, responder e encerrar conversas recebidas, exclusivamente dos atendimentos direcionados a esse atendente.
* Cada atendente acessará o aplicativo com seu próprio login e senha, cadastrados pelo administrador.
* O atendente deverá encerrar o atendimento (através do botão de encerrar), após encerrado, não poderá mais enviar mensagem.
* Se o atendente precisar dar retorno ao cliente, então ao invés de encerrar o atendimento, ele escolherá a opção de "aguardando retorno".
* O atendente não enviará mensagem de forma ativa, ele precisa primeiro receber a mensagem do cliente para poder responder.

* O sistema deve ser integrado APENAS com uma API oficial da Meta.
* Quando alguém enviar mensagem para a empresa, o chatboat apresentará um menu para que o cliente escolha um departamento. Caso o cliente responda qualquer coisa fora das opções, o chatbot retornará "opção inválida" e mostrará novamente o menu.
* O chatbot fará a transferência para um atendente dentro do departamento selecionado pelo cliente selecionando, quando houver mais de um atendente, o próximo atendente da fila (será definido por ordem de login, quando um atendente pegar um atendimento, ele volta para o final da fila).
* O sistema deverá armazenar o histórico da conversa e o telefone em um banco de dados.
* O sistema NÃO pode ser usado para marketing.