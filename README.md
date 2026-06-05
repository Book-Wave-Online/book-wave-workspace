# Arquitetura de Locação de Livros - MVP

Este repositório contém a fundação arquitetural para uma aplicação web responsiva de locação de livros. O projeto foi desenhado utilizando microsserviços, o padrão **BFF (Backend For Frontend)**, e autenticação robusta com **OAuth2**, garantindo escalabilidade, segurança e total desacoplamento entre as camadas.

---

## 1. Visão Geral e Objetivos do MVP

O principal objetivo desta arquitetura nesta fase de **MVP (Minimum Viable Product)** é validar as regras de negócio centrais de forma ágil, sem abrir mão de uma estrutura técnica que permita uma evolução fluida para produção.

* **Foco no Core Business:** Priorização dos fluxos essenciais de busca de títulos, consulta de disponibilidade e efetivação de empréstimos.
* **Segurança desde o Dia Um:** Centralização da identidade e proteção contra vulnerabilidades web clássicas (como XSS e CSRF) através do ecossistema de segurança configurado no Gateway.
* **Desacoplamento Técnico:** Isolamento de responsabilidades onde o frontend ignora a existência e a complexidade interna dos microsserviços em Java.

---

## 2. Stack Tecnológica do Sistema

A escolha das tecnologias visa alta performance, facilidade de manutenção e modularidade. Cada componente desempenha um papel estrito no ecossistema:

### 📱 Frontend Angular (`bw-fed-login`)
* **Papel:** Interface SPA (Single Page Application) totalmente responsiva e dedicada à experiência do usuário (UX) em ambiente web e mobile.
* **Segurança:** Comunicação com o backend protegida, delegando o armazenamento e gerenciamento de tokens sensíveis ao BFF.

### ⚙️ Backend BFF Node.js
* **Papel:** Camada intermediária de orquestração exclusiva para o frontend Angular. Formata as respostas exatamente como a interface necessita e centraliza a segurança.
* **Estratégia Cookie-to-Token:** Transforma o protocolo de segurança para que o cliente web consuma apenas cookies seguros (`HttpOnly` e `Secure`), atuando como o *Confidential Client* do fluxo OAuth2.

### ☕ Microsserviços Java (Spring Boot)
* **Papel:** Processamento do núcleo de negócio e garantia da consistência operacional.
* **Estrutura:** Serviços desacoplados e independentes (ex: *Catalog Service* e *Rental Service*) criados sobre o ecossistema robusto do Spring Cloud.

### 🍃 Banco de Dados MongoDB
* **Papel:** Persistência NoSQL de alta performance orientada a documentos.
* **Evolução Ágil:** Permite esquemas de dados flexíveis e dinâmicos, ideais para o ritmo de alteração de um MVP. No início, adota-se o isolamento lógico das coleções em uma única instância para otimização de custo e infraestrutura.
