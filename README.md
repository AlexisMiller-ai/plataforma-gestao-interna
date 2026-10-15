# Plataforma de Gestão Interna

> Vitrine de um sistema em produção na **Exclusive Beauty** (Recife, PE). O código é privado, da empresa. Aqui estão o que o sistema faz, como foi construído e as telas, com os dados ocultos.

O ponto da equipe era em papel, as horas eram somadas na mão e as rotinas, tarefas e avisos ficavam espalhados entre planilhas e grupos de mensagem. A plataforma reuniu tudo em um painel só: cada pessoa bate o ponto, acompanha a própria rotina e as próprias tarefas, e a gestão enxerga a equipe inteira com o saldo de horas já calculado.

<p>
  <img src="https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=react&logoColor=black" />
  <img src="https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white" />
  <img src="https://img.shields.io/badge/Tailwind_CSS-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white" />
  <img src="https://img.shields.io/badge/Vite-646CFF?style=for-the-badge&logo=vite&logoColor=white" />
  <img src="https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white" />
  <img src="https://img.shields.io/badge/Express-000000?style=for-the-badge&logo=express&logoColor=white" />
  <img src="https://img.shields.io/badge/PostgreSQL_(Supabase)-4169E1?style=for-the-badge&logo=postgresql&logoColor=white" />
  <img src="https://img.shields.io/badge/JWT-000000?style=for-the-badge&logo=jsonwebtokens&logoColor=white" />
  <img src="https://img.shields.io/badge/Vercel-000000?style=for-the-badge&logo=vercel&logoColor=white" />
</p>

## O que o sistema faz

- **Ponto digital** — cada pessoa registra entrada e saída pelo próprio painel, no lugar do ponto em papel. A gestão vê a semana ou o mês da equipe, com a situação de cada um em uma frase ("Em dia", "Deve 5h30"), e pode corrigir qualquer dia.
- **Escala individual** — a jornada prevista de cada pessoa, dia a dia. A meta de horas vem da escala e não de uma carga fixa igual para todos.
- **Rotinas** — a gestão monta a rotina fixa de cada colaborador, e a pessoa marca no quadro semanal o que cumpriu.
- **Tarefas em kanban, relatórios diários com exportação em PDF, mural de comunicados e chat interno** — o resto do dia a dia da equipe.

## Regras de negócio do banco de horas

A parte mais trabalhosa foi acertar a conta de horas para que ela fosse justa e batesse com a realidade:

- As somas da semana e do mês descontam o almoço só nos dias com mais de 6 horas.
- A meta acompanha o calendário e a escala de cada pessoa: 6h por dia dão 126h em um mês e 132h em outro.
- Hora a menos sempre conta como débito. Hora a mais só vira crédito quando a gestão marca como hora extra combinada.
- Atestados, folgas e feriados saem do previsto em vez de virar dívida. Feriado é cadastrado uma vez e vale para a equipe toda.
- Quem é desligado tem a conta congelada no último dia trabalhado, e o histórico continua consultável.
- A mesma regra existe no frontend e no backend, e um teste automatizado roda os mesmos cenários nas duas implementações para garantir que elas não divergem.

## Segurança e acesso

- **Autenticação JWT própria**, com senhas guardadas com bcrypt. Quem foi desligado não consegue mais entrar.
- **Dois perfis de acesso** (administrador e colaborador): cada pessoa vê apenas os próprios dados, e só a gestão vê a equipe inteira.
- **O frontend nunca fala direto com o banco.** Todo acesso passa pela API em Express, e o banco tem Row Level Security ligado em todas as tabelas.

## Telas

> Os dados da equipe foram ocultados.

<!-- Adicione os prints na pasta screenshots/ e descomente as linhas abaixo -->
<!--
<img src="screenshots/ponto.png" width="100%" />
<img src="screenshots/tarefas.png" width="100%" />
<img src="screenshots/relatorio.png" width="100%" />
-->

---

Desenvolvido por [Alexis Prado](https://github.com/AlexisMiller-ai).
