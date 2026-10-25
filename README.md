# Suporte Rápido — Painel de Manutenção Windows

Painel de ferramentas para o dia a dia do suporte: acesso remoto, senhas, bloqueio de conta,
Active Directory, cache de navegador, rede e manutenção rápida.

## Como usar

1. Abra o `index.html` com duplo clique (Chrome, Edge ou Firefox). Não precisa instalar nada,
   não precisa de servidor e funciona offline.
2. Preencha o **Contexto** no topo (usuário, host, IP, domínio, senha temporária). Todos os
   scripts passam a sair prontos, com `{{host}}` etc. já substituídos.
3. Busque pelo sintoma (`bloqueio`, `cache`, `lento`) ou pelo comando (`4740`, `mstsc`).
4. **Copiar** → cole no PowerShell/CMD do PC. **Baixar** → gera `.ps1`, `.bat` ou `.rdp` pronto.
5. Registre o atendimento na aba **Chamados** e acompanhe os passos nos **Checklists**.

## Abas

| Aba | O que tem |
|---|---|
| Ferramentas | 122 scripts/comandos em 8 categorias |
| Chamados | Fila de atendimentos (título, usuário, host, prioridade, status, notas) |
| Checklists | 7 fluxos passo a passo com progresso salvo |
| Configurações | Exportar/Importar JSON, criar ferramentas próprias, apagar dados |

## Categorias

- **Acesso Remoto** — mstsc, RDP com .rdp pronto, Quick Assist, msra, PowerShell remoto,
  WinRM, PsExec, WMI, tarefas remotas, sessões (`quser`/`rwinsta`), shares `C$`, portproxy.
- **Senhas & Contas** — reset no AD (e por interface), Entra/M365, conta local, desbloquear,
  força de troca no logon, senha em massa via CSV, geradores de senha, Wi-Fi e credenciais salvas.
- **Bloqueio de Conta** — PDC/FSMO, evento 4740, 4625/4771 (origem do erro), `BadPwdCount`,
  desbloqueio em massa, política de lockout, credenciais obsoletas e fluxo de investigação.
- **Active Directory** — `gpupdate`/`gpresult`, rejoin e canal seguro, `dcdiag`, `repadmin`,
  DNS SRV, perfis corrompidos, SYSVOL, sincronia de relógio, relatórios de inativos.
- **Navegador & Cache** — limpeza de cache sem perder login, perfil corrompido, modo limpo,
  políticas de GPO no navegador, atualização por `winget`, diagnóstico de site que não abre.
- **Rede** — diagnóstico completo, DNS, portas, reset de WinStack/IP, IP duplicado, proxy,
  Wi-Fi, firewall, `netstat`, VPN e acesso a shares.
- **Manutenção Rápida** — SFC/DISM, reset do Windows Update, spooler de impressão, limpeza
  de disco, Explorer, boot lento, serviços parados, logs, ponto de restauração, backup de
  dados, Office/Teams, Store, CHKDSK, permissões, licenciamento e coleta de diagnóstico.
- **Utilitários** — cheat sheet de teclas, atalhos `ms-settings`, `msg` para a tela do usuário,
  elevação de privilégios, ficha técnica do PC e aviso com contagem regressiva.

## Atalhos

- `Ctrl + K` — busca
- `Esc` — limpa a busca
- `Ctrl + Shift + C` — copia a primeira ferramenta visível

## Dados e privacidade

Tudo fica no `localStorage` do próprio navegador. **Exportar** gera um `.json` com contexto,
chamados, checklists e ferramentas criadas — importe em outra máquina para compartilhar.
O painel **não executa** comandos: ele só monta, copia e gera os scripts.
