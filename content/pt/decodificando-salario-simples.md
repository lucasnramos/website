+++
title = "Projeto: Salário Simples"
description = "Decodificando o Salário Simples: por trás do comparador CLT vs. PJ"
date = "2026-04-10"
+++

# Decodificando o Salário Simples: por trás do comparador CLT vs. PJ

Escolher entre um emprego CLT e uma proposta como PJ é um dos maiores dilemas para profissionais no Brasil. Para resolver isso com dados, criamos o **Salário Simples**, uma aplicação que automatiza esses cálculos complexos. Aqui vai um resumo da tecnologia e da lógica por trás da ferramenta.

## Stack de tecnologia

* **Next.js 16 (App Router):** uso otimizado de componentes server/client
* **React 19:** melhorias de performance e novos recursos
* **TypeScript:** segurança de tipos e precisão nos cálculos financeiros
* **Tailwind CSS 4:** interface responsiva com suporte nativo a modo escuro

## Lógica de negócio

A complexidade está nas regras tributárias brasileiras, divididas em dois módulos:

### CLT

O motor de cálculo processa **INSS** e **IRRF** progressivos, incluindo deduções. Além do salário líquido mensal, projeta a renda anual com **13º salário** e **férias**, oferecendo uma visão mais realista dos ganhos.

### PJ (Simples Nacional)

Focado no **Simples Nacional (Anexo V)**, inclui:

* **Fator R:** padrão de 28% via pró-labore para otimização tributária
* **Impostos corporativos:** cálculo automático da alíquota efetiva
* **Dupla tributação:** considera impostos pessoais e da empresa para mostrar o lucro líquido real

### Equivalência CLT vs. PJ

Um diferencial é a busca de equivalência: usando **busca binária**, o sistema calcula rapidamente quanto um PJ precisa faturar para igualar o rendimento líquido anual de um CLT.

## Deploy e CI/CD

* **GitHub Actions:** valida código (lint + build) a cada alteração
* **Vercel:** deploy automático com previews por branch

## Conclusão

O Salário Simples mostra que ferramentas financeiras podem ser simples e claras, ajudando na tomada de decisão de carreira.

👉 Acesse: [https://salario-simples.lucasnramos.com](https://salario-simples.lucasnramos.com)

