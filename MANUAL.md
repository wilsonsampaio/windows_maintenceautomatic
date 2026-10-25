# 📖 Manual do Usuário — Suporte Rápido

**Painel de manutenção Windows · Active Directory · Senhas · Acesso remoto**

Este manual ensina, do zero e passo a passo, a usar todas as funções do painel: como preencher o
Contexto, como buscar e copiar comandos, como gerar arquivos executáveis, como registrar
chamados, como seguir os checklists e como resolver os problemas mais comuns do atendimento.

> Público-alvo: analistas de suporte N1/N2, técnicos de campo e líderes de help desk.
> Pré-requisito para os comandos de domínio: acesso administrativo e, quando indicado, RSAT
> (ferramentas de administração remota do Active Directory).

---

## Sumário

1. [Primeiros passos](#1-primeiros-passos)
2. [Anatomia da tela](#2-anatomia-da-tela)
3. [O Contexto do atendimento](#3-o-contexto-do-atendimento)
4. [Aba Ferramentas](#4-aba-ferramentas)
5. [Como executar os scripts com segurança](#5-como-executar-os-scripts-com-segurança)
6. [Aba Chamados](#6-aba-chamados)
7. [Aba Checklists](#7-aba-checklists)
8. [Aba Configurações](#8-aba-configurações)
9. [Atalhos de teclado](#9-atalhos-de-teclado)
10. [Fluxos práticos de atendimento](#10-fluxos-práticos-de-atendimento)
11. [Boas práticas e segurança](#11-boas-práticas-e-segurança)
12. [Solução de problemas do painel](#12-solução-de-problemas-do-painel)
13. [Glossário](#13-glossário)
14. [Referência rápida de comandos](#14-referência-rápida-de-comandos)

---

## 1. Primeiros passos

1. Pegue o arquivo `index.html` (repositório ou cópia na rede) e **abra com duplo clique** no
   navegador do seu posto. Não há instalação, não há servidor e não é preciso internet.
2. Assim que abrir, aparece a aba **Ferramentas** com os 122 comandos agrupados por categoria.
3. Antes de qualquer coisa, preencha a **faixa de Contexto** no topo (seção 3). Isso poupa
   digitação em todos os cartões.
4. Use a **busca** (`Ctrl+K`) para achar a ferramenta — pelo sintoma ou pelo comando.
5. Ao final do atendimento, registre-o na aba **Chamados**.

**Se o painel abrir em branco ou desconfigurado:** pressione `Ctrl+Shift+R` (recarga dura) ou
apague os dados em *Configurações → Apagar dados* (seção 12).

---

## 2. Anatomia da tela

| Região | Onde fica | Para que serve |
|---|---|---|
| **Barra lateral** | Esquerda | Alterna entre as 4 abas, mostra as 8 categorias com contagem e traz a dica de uso/atalhos |
| **Busca** | Topo | Filtra as ferramentas por qualquer palavra (título, descrição, tag, comando, categoria) |
| **Contexto** | Logo abaixo da busca | Dados do atendimento aplicados a todos os scripts |
| **Contador de pendências** | Ao lado de *Chamados* | Número de chamados que ainda não estão como *Resolvido* |
| **Cartão de ferramenta** | Área principal | Uma ferramenta: selo de risco, título, descrição, campos, script e botões |
| **Rodapé do cartão** | Base do cartão | Linguagem (`PS`, `CMD`, `RDP`, `URL`, `TXT`), tags, **Baixar** e **Copiar** |

No celular a barra lateral vira um botão **☰ Menu** e os cartões ficam em coluna única.

---

## 3. O Contexto do atendimento

O Contexto é o coração da produtividade do painel: você digita os dados **uma vez** e todos os
scripts já saem montados.

| Campo | Variável | Exemplo | Observação |
|---|---|---|---|
| Usuário | `{{usuario}}` | `jsilva` | Nome de usuário (SAM), sem domínio |
| Host | `{{host}}` | `PC-ABC123` | Nome da máquina alvo |
| IP | `{{ip}}` | `10.0.1.55` | Endereço da máquina |
| Domínio | `{{dominio}}` | `empresa.local` | Domínio FQDN |
| Senha temporária | `{{senha}}` | `••••••••` | Fica mascarada na tela |

Regras importantes:

- **Campo vazio vira `<host>`** no script. É um lembrete: falta preencher.
- **O campo do cartão tem prioridade** sobre o Contexto. Preencheu errado no Contexto? Corrija
  só naquele cartão, sem afetar os demais.
- **Variáveis novas**: qualquer `{{outra_variavel}}` que apareça no corpo de uma ferramenta gera
  um campo editável próprio naquele cartão (útil nas ferramentas personalizadas).
- **A senha sai junto** do script quando o comando usa `{{senha}}`. Depois do atendimento, limpe
  o campo.

---

## 4. Aba Ferramentas

![Visão geral](docs/screenshots/01-ferramentas.png)

### 4.1 Navegando pelas categorias

Clique numa categoria da barra lateral para ver só aquilo; **Todas** volta à visão completa. Cada
seção mostra a contagem de ferramentas à direita.

### 4.2 O que tem em cada cartão

```
[SEGURO]  Abrir RDP no host do usuário          ← selo de risco + título
Sessão Remote Desktop completa no PC informado. ← para que serve
HOST / IP
[PC-ABC123]                                     ← campo editável (vem do Contexto)
┌─────────────────────────────────────────────┐
│ mstsc /v:PC-ABC123 /f                       │ ← script pronto (área rolável)
└─────────────────────────────────────────────┘
CMD   mstsc  rdp  remoto        [Baixar] [Copiar]
      linguagem  tags              ações
```

- **Selo de risco** (ver seção 4.5) — olhe antes de colar.
- **Campos** — ajuste host, usuário, porta, dias, nome do serviço, conforme a ferramenta.
- **Bloco de código** — é o que vai para a área de transferência; rola na horizontal se o
  comando for longo.
- **Baixar** — gera um arquivo (seção 4.4). Em ferramentas do tipo *link*, o botão aparece como
  **Abrir** e abre a página/protocolo direto.

### 4.3 Buscando

A busca varre título, descrição, tags, corpo do comando e categoria. Exemplos práticos:

| Digite | Resultado típico |
|---|---|
| `4740` | evento de lockout e origem |
| `mstsc` | comandos de RDP e o `.rdp` pronto |
| `cache` | limpeza de cache do navegador e do DNS |
| `bloqueio` | desbloqueio, política, investigação, credencial velha |
| `spooler` | impressão |
| `lento` / `boot` | desempenho e inicialização |
| `reset` | Windows Update, Edge, Teams, Store, Winsock |
| `perfil` | perfil de usuário e de navegador corrompidos |
| `wifi` | status, senha e perfil de rede sem fio |

`Esc` limpa a busca; `Ctrl+K` volta o foco para ela.

### 4.4 Copiar e Baixar

| Botão | O que faz | Quando usar |
|---|---|---|
| **Copiar** | Leva o script preenchido para a área de transferência | Você vai colar no PowerShell/CMD do PC |
| **Baixar** | Gera um arquivo no seu posto | Você quer guardar, mandar para outro técnico ou rodar depois |
| **Abrir** (ferramentas-link) | Abre o protocolo/página | Quick Assist, tela de senhas do navegador, `about:support` |

Arquivos gerados:

| Linguagem | Extensão | Como executar |
|---|---|---|
| `PS` | `.ps1` | botão direito → **Executar com o PowerShell** (ou `powershell -File arquivo.ps1`) |
| `CMD`/`BAT` | `.bat` | duplo clique; use *Executar como administrador* quando pedir |
| `RDP` | `.rdp` | duplo clique abre o mstsc já configurado com impressoras/drives |
| `TXT` | `.txt` | bloco de notas (passo a passo, cheat sheets) |

### 4.5 Selos de risco

| Selo | Significado | Exemplos |
|---|---|---|
| 🟢 **SEGURO** | Consulta/leitura; não altera nada | `gpupdate`, eventos, `ping`, ficha técnica |
| 🟡 **ATENÇÃO** | Altera estado no PC ou no domínio | reset de senha, limpar credenciais, apagar cache, renomear perfil |
| 🔴 **CRÍTICO** | Pode derrubar sessão, mudar boot, apagar dados ou quebrar acesso | `rwinsta`, desligar remoto, `icacls`, modo seguro, rejoin de domínio |

---

## 5. Como executar os scripts com segurança

1. **Abra o terminal como administrador**: `Win+X` → *Terminal (Administrador)* ou
   *PowerShell (Administrador)*.
2. **PowerShell pode bloquear script baixado** (Execution Policy). Duas saídas seguras:
   ```powershell
   # executa apenas este arquivo, sem mudar política global
   powershell -NoProfile -ExecutionPolicy Bypass -File .\nome-do-script.ps1

   # ou, dentro da sessão:
   Set-ExecutionPolicy -Scope Process Bypass
   ```
3. **SmartScreen do Windows** pode avisar ao abrir `.bat`/`.ps1` baixado:
   *Mais informações* → *Executar assim mesmo* (só para arquivo de origem confiável).
4. **Comandos de domínio** exigem o módulo do Active Directory (RSAT):
   ```powershell
   Get-Module -ListAvailable ActiveDirectory
   # se faltar, no Windows client:
   Add-WindowsCapability -Online -Name Rsat.ActiveDirectory.DS-LDS.Tools~~~~0.0.1.0
   ```
5. **PowerShell remoto** (`Enter-PSSession`) exige WinRM habilitado no destino — use a
   ferramenta *Habilitar WinRM no destino* (rode no PC do usuário, como admin).
6. **Leia o comando antes de colar.** Selos 🟡 e 🔴 merecem 10 segundos de leitura.

---

## 6. Aba Chamados

![Chamados](docs/screenshots/04-chamados.png)

Serve para registrar o que foi feito, sem depender do sistema de tickets da empresa.

**Criar:** preencha *Título* (obrigatório), *Usuário* e *Host* (já vêm do Contexto), escolha
*Prioridade* e *Status*, escreva as *Notas* e clique em **Adicionar chamado**.

**Status possíveis:** `Aberto` → `Em andamento` → `Aguardando usuário` → `Resolvido`.
Altere pelo seletor dentro do próprio cartão da fila.

**A fila:** barra lateral colorida por prioridade (🔴 alta, 🟡 média, 🟢 baixa), com data, notas
visíveis, seletor de status e botão *Excluir*.

**Botões do topo da fila:**

- **Exportar fila (.json)** — baixa só os chamados (o botão *Exportar* da barra superior baixa
  tudo, incluindo ferramentas e checklists).
- **Limpar resolvidos** — remove tudo que está *Resolvido* (pede confirmação).

**Estatísticas:** caixinhas no topo mostram abertos, em andamento, aguardando, resolvidos e total;
o mesmo número de pendências aparece ao lado de *Chamados* na barra lateral.

---

## 7. Aba Checklists

![Checklists](docs/screenshots/05-checklists.png)

São 7 fluxos operacionais com passos na ordem certa:

| Checklist | Passos | Uso |
|---|---:|---|
| 1 · Triagem do atendimento | 7 | sempre, em todo chamado novo |
| 2 · Bloqueio de conta | 11 | conta bloqueada no AD |
| 3 · Troca / recuperação de senha | 10 | reset de senha |
| 4 · PC lento | 11 | desempenho |
| 5 · Navegador com problema | 12 | cache, perfil, site |
| 6 · Sem internet / rede | 11 | conectividade |
| 7 · Novo PC / onboarding | 13 | entrega de máquina |

Como usar:

- **Clique no item** (ou na caixa) para marcar — o texto riscado e a barra de progresso atualizam
  na hora.
- O progresso é **salvo por checklist**, então dá para parar no meio e voltar depois.
- **Reiniciar** zera o checklist para o próximo atendimento do mesmo tipo.
- Some a barra lateral de prioridade do chamado com o checklist: um atendimento fica rastreável do
  começo ao fim.

---

## 8. Aba Configurações

![Configurações](docs/screenshots/06-configuracoes.png)

### 8.1 Backup e sincronização

| Botão | O que faz |
|---|---|
| **Exportar JSON** | Baixa `suporte-rapido-backup.json` com Contexto, ferramentas criadas, chamados, checklists e preferências |
| **Importar JSON** | Lê o arquivo e mescla tudo no navegador atual (sobrescreve chamados/ferramentas com os do arquivo) |
| **Apagar dados** | Zera o `localStorage` do painel (pede confirmação; use ao trocar de posto ou por segurança) |

**Rotina sugerida para a equipe:** no fim do expediente quem lidera exporta o JSON e guarda na
rede; na segunda-feira todo mundo importa. Assim a fila fica compartilhada sem servidor.

### 8.2 Nova ferramenta (personalizada)

Preencha *Título*, *Categoria*, *Risco*, *Linguagem*, *Descrição* e o *Corpo*, e clique em
**Adicionar ferramenta**.

- No corpo, use `{{variavel}}` para cada valor variável: o painel **cria sozinho um campo
  editável** no cartão.
- Exemplo:
  ```powershell
  Restart-Service -Name '{{servico}}' -Force
  Get-Service {{servico}} | Format-Table Name,Status
  ```
- A ferramenta aparece com o selo roxo **meu** e pode ser excluída pelo próprio cartão.

### 8.3 Como usar o painel / atalhos

O terceiro bloco repete o resumo de uso, o aviso de segurança e os atalhos — bom para treinar
novo analista.

---

## 9. Atalhos de teclado

| Atalho | Ação |
|---|---|
| `Ctrl + K` | Foca na busca (e retorna para a aba Ferramentas) |
| `Esc` | Limpa a busca |
| `Ctrl + Shift + C` | Copia a primeira ferramenta visível |

**Windows, para passar ao usuário** (ferramenta *Cheat sheet: atalhos de teclado*):

| Atalho | Uso |
|---|---|
| `Win + X` | menu administrativo (PowerShell/Terminal admin) |
| `Win + R` | Executar (`dsa.msc`, `services.msc`) |
| `Ctrl + Shift + Esc` | gerenciador de tarefas direto |
| `Win + L` | bloquear estação |
| `Win + Shift + S` | captura de tela |
| `Alt + F4` | fechar janela (no desktop: desligar) |
| `Win + P` | projetar/tela dupla |

---

## 10. Fluxos práticos de atendimento

### 10.1 Conta de senha bloqueada

1. Valide a identidade do solicitante (ramal + gestor, conforme política).
2. Preencha o Contexto com o usuário e o host.
3. Busque `bloqueio` → rode **Descobrir o DC (PDC Emulator)** e **Diagnóstico completo da conta**.
4. Busque `4740` → rode **Quem bloqueou? Evento 4740** no DC e anote a máquina de origem.
5. Se precisar do IP de origem: **De onde vem a senha errada (4771 / 4625)**.
6. **Desbloquear conta no AD** (`Unlock-ADAccount`).
7. **Resetar senha** + troca no próximo logon.
8. **Limpar credenciais salvas** no PC do usuário e orientar redesenho do e-mail no celular.
9. Abra a aba *Checklists* → *2 · Bloqueio de conta* e marque cada passo.
10. Registre tudo em *Chamados* (origem, causa, ação) e teste com o usuário.

### 10.2 Troca de senha (remota)

1. Contexto: usuário, host, domínio.
2. Busque `reset` → **Resetar senha de conta no AD** (ou **pela interface** para quem usa ADUC).
3. Mantenha **Forçar troca de senha no próximo logon**.
4. Busque `credencial` → limpe a senha antiga salva (cmdkey/keymgr) no posto do usuário.
5. Peça logoff/logon e confirme o acesso a rede, e-mail e ERP.
6. Checklists → *3 · Troca / recuperação de senha*.

### 10.3 Conectar na máquina do usuário

| Situação | Ferramenta |
|---|---|
| Preciso ver a tela dele | **Quick Assist** (gera código) ou **Assistência Remota** (`msra`) |
| Tenho acesso de admin e quero assumir a sessão atual | **RDP em modo console** (`mstsc /v:host /admin`) |
| Quero abrir sessão normal | **Abrir RDP no host do usuário** |
| Quero deixar um .rdp configurado para o time | **Arquivo .rdp com impressoras, drives e console** |
| Só preciso rodar um comando | **CMD remoto com PsExec**, **Executar processo remoto via WMI** ou **Agendar tarefa remota** |
| Preciso ver quem está logado / derrubar sessão | **Ver quem está logado** e **Derrubar sessão** (use com aviso!) |

Antes de tudo, **Verificar se RDP/WinRM responde no host** evita tentativa à toa.

### 10.4 Navegador com problema

1. Descubra a versão (`chrome://version` ou botão **Abrir** de *Senhas salvas*).
2. Teste em aba anônima (`Ctrl+Shift+N`) para isolar extensão.
3. Busque `cache` → **Fechar navegador e limpar cache** (ou **Apagar só o cache** para manter login).
4. `ipconfig /flushdns` (ferramenta **Limpar cache de DNS**) e teste de novo.
5. Persistindo: **Navegador corrompido: criar perfil novo** e depois **Recuperar abas/favoritos**.
6. Checklists → *5 · Navegador com problema*.

### 10.5 PC lento

1. Busque `lento` → **Diagnóstico / verifique disco** (`Get-Volume`, espaço livre).
2. **Por que o PC demora para ligar** (tempo de boot e inicialização).
3. **Programas que abrem com o Windows** (desative só o que conhecer).
4. **Serviços essenciais parados** e **Erros recentes do Windows**.
5. **Limpeza de disco** + **Limpar temporários**.
6. Se suspeitar de corrupção: **Reparar arquivos do Windows (SFC + DISM)**.
7. Checklists → *4 · PC lento*; ao final, **Coletar diagnóstico completo** se escalar.

### 10.6 Sem internet

1. **Diagnóstico de rede completo (1 comando)**.
2. Ping do gateway e depois de `8.8.8.8` → onde quebra?
3. `ipconfig /flushdns` → se só falha por nome, é DNS.
4. Conferir IP (`169.254.x.x` = sem DHCP) → **Renovar IP DHCP**.
5. Verificar **proxy** e **Wi-Fi**.
6. Persistindo: **Reset de WinStack + IP** (pede reinício).
7. Checklists → *6 · Sem internet / rede*.

### 10.7 Impressão com fila travada

1. Busque `spooler` → **Consertar impressão** (para o serviço, apaga a fila, volta a subir).
2. Se precisar: **Impressora não imprime / sai na porta errada** (porta, driver, padrão).
3. Avise o usuário antes — os jobs pendentes são descartados.

---

## 11. Boas práticas e segurança

- **Valide sempre a identidade** antes de resetar senha, desbloquear conta ou liberar RDP.
- **Olhe o selo de risco** antes de colar; leia o comando inteiro nos selos 🔴.
- **Prefira troca no logon** a senha temporária fixa.
- **Não envie senha por chat aberto** — use o canal aprovado pela empresa.
- **Limpe o Contexto** ao terminar o atendimento (especialmente o campo de senha).
- **Anote a origem** em caso de bloqueio: sem origem, o problema volta em minutos.
- **Não exporte JSON** contendo dados sensíveis para locais não autorizados.
- **Crie ponto de restauração** antes de driver, update grande ou mudança de registro.
- **Backup antes de mexer**: use **Backup rápido dos dados do usuário** em manutenção pesada.
- O painel é **apoio, não automação**: quem executa é você, com os privilégios adequados.

---

## 12. Solução de problemas do painel

| Sintoma | Causa provável | Solução |
|---|---|---|
| Tela em branco ao abrir | JavaScript bloqueado ou navegador antigo | Use Chrome/Edge/Firefox atual; `Ctrl+Shift+R` |
| Os campos do Contexto aparecem vazios | Dados apagados ou navegador diferente | Preencha de novo (cada navegador guarda o seu) |
| Script aparece com `<host>` | Campo do Contexto vazio | Preencha o Contexto ou o campo do cartão |
| Nada encontrado na busca | termo muito específico | Tente palavra mais curta: `dns`, `cache`, `reset` |
| Botão **Copiar** não funciona | permissão de área de transferência | Use `Ctrl+C` selecionando o bloco, ou **Baixar** |
| **Baixar** não salva | download bloqueado pelo navegador | Libere download para este site/arquivo |
| Ferramenta personalizada sumiu | `localStorage` limpo | Importe o JSON de backup |
| Os chamados de outro PC não aparecem | dados são locais ao navegador | *Configurações → Importar JSON* |
| Script `.ps1` não abre Execution Policy | política restritiva | `powershell -ExecutionPolicy Bypass -File .\arquivo.ps1` |
| Comando de domínio falha com "cmdlet não reconhecido" | RSAT ausente | Instale a capacidade `Rsat.ActiveDirectory` (seção 5) |
| `Enter-PSSession` pede recursão/WinRM | WinRM desligado no destino | Rode **Habilitar WinRM no destino** no PC do usuário |
| A senha apareceu no script ao copiar | o comando usa `{{senha}}` | Limpe o campo de senha do Contexto depois de copiar |
| Quero zerar tudo | — | *Configurações → Apagar dados* |

---

## 13. Glossário

| Termo | Significado |
|---|---|
| **AD** | Active Directory — diretório de usuários/computadores do domínio |
| **ADUC** | *Active Directory Users and Computers* — interface gráfica (`dsa.msc`) |
| **DC** | Domain Controller — servidor que autentica o domínio |
| **PDC Emulator** | DC que processa alterações de senha e lockout da maioria das contas |
| **FSMO** | 5 papéis mestres do AD (confira com `netdom query fsmo`) |
| **GPO** | Group Policy Object — política aplicada por `gpupdate /force` |
| **Lockout** | Bloqueio de conta por excesso de tentativas de senha errada |
| **4740** | Evento de segurança "conta bloqueada" (traz a máquina de origem) |
| **4625 / 4771** | Falha de logon / falha Kerberos (trazem IP e estação) |
| **BadPwdCount** | Quantas senhas erradas a conta tem registradas |
| **mstsc** | Cliente de Área de Trabalho Remota do Windows (RDP) |
| **WinRM** | Serviço de gerenciamento remoto do PowerShell (porta 5985/5986) |
| **Kerberos** | Protocolo de autenticação do domínio; sofre com relógio dessincronizado |
| **SPN** | *Service Principal Name* — identidade de serviço no AD |
| **SFC / DISM** | Ferramentas de reparo da imagem e dos arquivos do Windows |
| **Spooler** | Serviço de impressão (`Print Spooler`) |
| **Share `C$`** | Compartilhamento administrativo do disco C (`\\host\C$`) |
| **RSAT** | Ferramentas remotas de administração (módulo `ActiveDirectory`) |
| **Entra ID** | Antigo Azure AD — identidades em nuvem do Microsoft 365 |
| **DPAPI** | Criptografia local do Windows usada pelo navegador no cofre de senhas |
| **JSON** | Formato do arquivo de exportação/importação do painel |

---

## 14. Referência rápida de comandos

| Necessidade | Comando |
|---|---|
| Atualizar GPO | `gpupdate /force` |
| Ver GPO aplicadas | `gpresult /r` (ou `/h relatorio.html`) |
| DC do domínio | `netdom query fsmo` |
| Status da conta | `Get-ADUser <u> -Properties Enabled,LockedOut,PasswordLastSet` |
| Desbloquear | `Unlock-ADAccount -Identity <u>` |
| Resetar senha | `Set-ADAccountPassword <u> -Reset -NewPassword (ConvertTo-SecureString '...' -AsPlainText -Force)` |
| Forçar troca | `Set-ADUser <u> -ChangePasswordAtLogon $true` |
| Evento de lockout | `Get-WinEvent -FilterHashtable @{LogName='Security';Id=4740;StartTime=(Get-Date).AddDays(-3)}` |
| Canal seguro | `Test-ComputerSecureChannel -Repair` |
| Replicação | `repadmin /replsummary` |
| Saúde do DC | `dcdiag /v` |
| DNS do domínio | `Resolve-DnsName -Type SRV _ldap._tcp.dc._msdcs.<dominio>` |
| RDP | `mstsc /v:<host> /admin` |
| Sessões | `quser` · `rwinsta <id> /server:<host>` |
| Cache DNS | `ipconfig /flushdns` |
| Teste de porta | `Test-NetConnection <host> -Port <porta>` |
| Reset de rede | `netsh winsock reset` + `netsh int ip reset` + reinício |
| Reparo do Windows | `DISM /Online /Cleanup-Image /RestoreHealth` e `sfc /scannow` |
| Fila de impressão | `net stop spooler` → apagar `PRINTERS\*` → `net start spooler` |
| Espaço em disco | `Get-Volume C` |
| Erros recentes | `Get-WinEvent -FilterHashtable @{Level=1,2;StartTime=(Get-Date).AddHours(-24)}` |
| Relógio | `w32tm /resync /force` |
| Credenciais salvas | `cmdkey /list` · `control keymgr.dll` |
| Senha do Wi-Fi | `netsh wlan show profile name="<ssid>" key=clear` |

---

<div align="center">
<b>Fim do manual</b> · dúvidas sobre o painel: veja a seção 12 · melhorias: abra uma issue no repositório
</div>
