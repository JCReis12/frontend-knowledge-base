# Resumo completo de estudo — Aula 04: Consumindo APIs no Front-end

Este resumo reúne os conceitos de comunicação entre front-end e back-end, APIs REST, protocolo HTTP, endpoints e JSON, além da criação e publicação de uma API com Express. O objetivo é entender o caminho percorrido pelos dados entre a interface, o servidor e eventuais serviços externos.

## 1. API e API REST

**API** (*Application Programming Interface*, ou Interface de Programação de Aplicações) é um conjunto de regras e recursos que permite que componentes ou sistemas diferentes se comuniquem. Ela define como solicitar funcionalidades ou dados sem que o consumidor precise conhecer todos os detalhes internos do sistema que os fornece.

**REST** (*Representational State Transfer*) é um estilo arquitetural usado com frequência para construir APIs web. Uma API REST organiza a comunicação em torno de recursos identificados por URIs, utiliza os métodos HTTP de forma padronizada, troca representações desses recursos (comumente JSON) e mantém as requisições independentes umas das outras (*stateless*). Portanto, API é um conceito amplo; REST é uma das formas de projetar uma API.
