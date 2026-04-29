+++
title = "Project: Salário Simples"
description = "Decoding Salário Simples: Behind the CLT vs. PJ Calculator"
date = "2026-04-10"
+++

# Decoding Salário Simples: Behind the CLT vs. PJ Calculator

Choosing between a permanent (CLT) role and a contractor (PJ) proposal is one of the
biggest dilemmas for Brazilian professionals. To solve this with data, we created
<strong>Salário Simples</strong>, a modern application that automates these complex
calculations. In this article, we explore the technology and logic that power this tool.

## The Tech Stack

The project was built using the latest tools in the Web ecosystem:

- Next.js 16 (App Router): Leveraging optimized server and client components.
- React 19: Taking advantage of performance improvements and the library's new features.
- TypeScript: Ensuring type safety across all financial calculations and avoiding common precision errors.
- Tailwind CSS 4.0: For a responsive, clean interface with native Dark
- Mode support.

## Business Logic: The Heart of the App

The complexity of Salário Simples lies in the accuracy of Brazilian tax rules, divided into two main modules:

### 1. The CLT World

The calculation engine (<code>salaryCalculator.ts</code>) processes the
progressive <strong>INSS</strong> (social security) brackets and
<strong>IRRF</strong> (income tax) rates, including deductions for dependents.
Beyond monthly net pay, the app projects annual income by including the
<strong>13th salary</strong> and <strong>vacation bonuses</strong>, providing a
realistic view of total earnings.

### 2. The PJ Ecosystem (Simples Nacional)

In the PJ module (<code>pjCalculator.ts</code>), we focus on the
<strong>Simples Nacional (Annex V)</strong>. The logic includes:

- Factor R: Defaulted to 28% via Pro-labore for tax optimization.</li>
- Corporate Taxes: Automatic calculation of the effective tax rate based on annual revenue.
- Double Taxation Handling: The app deducts both personal taxes (INSS/IRRF on pro-labore) and corporate taxes to show the true net profit.
        
### 3. The "Magic" of PJ Equivalency

A standout feature is the equivalency search. Using a
<strong>binary search algorithm</strong> (running 30 iterations in milliseconds),
the system finds exactly how much you need to invoice as a PJ contractor to match
the annual net income of a specific CLT salary.

## Deployment and CI/CD: Automating the Workflow

To ensure every improvement reaches the user safely, we use a robust
<strong>CI/CD</strong> pipeline:

- <strong>GitHub Actions:</strong> Every Pull Request or Push to the main branch
triggers an automated workflow that runs <code>lint</code> (ESLint) and the Next.js
<code>build</code>. This ensures the code is healthy before it even leaves the
repository.

- <strong>Vercel Deployment:</strong> Once the code passes the GitHub Actions checks,
   Vercel handles the deployment. Native integration allows for "Deploy Previews" for
   every branch, making it easy to review new features.

## Conclusion

Salário Simples proves that financial tools don't have to be complex or uninviting.
With a solid stack and efficient algorithms, we provide clarity for career
decision-making.

Like the project? Check out project at: https://salario-simples.lucasnramos.com
