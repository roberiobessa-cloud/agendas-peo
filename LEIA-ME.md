# Agendas do Gestor — PEO

Sistema web com as agendas por área (Coordenador, Líderes, Pré, Pós, ASB, Posso Ajudar), acessível por computador e celular, com sincronização em tempo real.

## Como funciona
- **Arquivo:** `index.html` (arquivo único, sem outros arquivos de dados).
- **Hospedagem:** GitHub Pages, publicado a partir deste repositório (`roberiobessa-cloud/agendas-peo`).
- **Banco de dados:** Firebase Firestore do mesmo projeto usado no painel PEO (`peo-clinica-sim`), coleção `agendas_gestor`.
- **Login do administrador:** Firebase Authentication — o mesmo e-mail/senha do painel PEO. Só quem tem o papel (`role`) `admin` na coleção `users` consegue editar.

## Acesso
- **Visualização:** qualquer pessoa com o link vê todas as agendas, sem login, sempre atualizadas — se o admin editar em um celular, quem estiver olhando no computador vê a mudança na hora, sem precisar recarregar nada manualmente.
- **Administrador:** clique em "Área do Administrador" no topo, entre com e-mail e senha (login já existente do painel PEO). Só usuários com `role: admin` conseguem criar, editar e excluir áreas e rotinas.

## O que o administrador pode fazer
- Criar, editar e excluir **áreas** (ex.: adicionar uma nova agenda no futuro).
- Criar, editar e excluir **rotinas** dentro de cada área (horário, descrição, participantes, frequência).
- **Exportar backup (JSON):** baixa uma cópia de segurança do conteúdo atual — útil antes de fazer mudanças grandes.

Toda edição é gravada direto no Firestore. Não existe mais um passo de "republicar" ou substituir arquivo — a mudança aparece para todo mundo automaticamente.

## Sobre as regras de segurança do Firestore
Foi criada uma regra dedicada para a coleção `agendas_gestor`: leitura pública (`allow read: if true`) e escrita restrita a usuários autenticados com `role: admin` (mesma verificação usada no painel PEO). As regras das coleções existentes (`users`, `evaluations`) também foram ajustadas — antes estavam em modo de teste aberto (expirando em 01/08/2026), agora exigem login, sem mudar o comportamento do sistema de avaliação já em uso.

## Populando os dados iniciais
Na primeira publicação, a coleção `agendas_gestor` é povoada uma única vez com o conteúdo digitalizado do E-book PEO (as 6 agendas). Depois disso, todo o conteúdo passa a ser gerenciado pelo modo administrador dentro do próprio app.
