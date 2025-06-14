# Resumo para Estudo - Certificação Microsoft AZ-104 (administração identidades)

---

## 1. Autenticação e Identidade no Active Directory (on-premises)
- **Kerberos:** Protocolo seguro, utilizado em domínios modernos.
- **NTLM:** Protocolo mais antigo, menos seguro, usado em ambientes legados.
- ⚠️ Importante: O Microsoft Entra ID não utiliza LDAP, GPO, OU ou Kerberos.

---

## 2. Microsoft Entra ID (antigo Azure AD)
- Identidade na nuvem com autenticação moderna: OAuth 2.0, OpenID Connect, SAML, WS-Federation.
- Suporte a acesso condicional e restrições de firewall para controle de acesso.

---

## 3. Conceitos Fundamentais no Entra ID
- **Identidade:** Qualquer usuário, aplicativo ou dispositivo que pode ser autenticado.
- **Conta:** Identidade vinculada a uma pessoa (e-mail, nome).
- **Conta Microsoft (Entra ID):** Conta pessoal ou corporativa usada em serviços da Microsoft.
- **Locatário (Tenant):** Representa a organização no Entra ID.
- **Assinatura do Azure:** Contrato de cobrança pelos recursos utilizados.

---

## 4. Planos do Microsoft Entra ID
| Plano    | Recursos                                                                                       |
|----------|------------------------------------------------------------------------------------------------|
| Gratuito | Logon único, autenticação multifator (MFA), portal de autoatendimento                         |
| P1       | Tudo do Gratuito + gerenciamento avançado de grupos, autenticação na nuvem federada, acesso condicional, provisionamento automático |
| P2       | Tudo do P1 + gerenciamento de identidade com privilégios (PIM), acesso baseado em risco       |

- Importante: PIM e provisionamento automatizado de usuários e grupos para aplicativos são cruciais para governança e segurança.

---

## 5. Gerenciamento de Identidades de Dispositivos
- BYOD (Bring Your Own Device): Registro de dispositivos pessoais com controle via MDM (ex: Intune).
- Dispositivos corporativos: Ingressam no Entra ID; políticas e login com conta organizacional.
- Legado (Windows 7+): GPOs e imagens personalizadas.

---

## 6. SSPR (Self-Service Password Reset)
- Passos para implementar o SSPR:
  - Determinar quem pode usar a redefinição de senha de autoatendimento
  - Definir número de métodos de autenticação: e-mail, telefone, perguntas de segurança, app autenticador.
  - Exigir registro (igual ao MFA).

- Como configurar:  
  Entra Portal → Usuários → Redefinição de senha  
  Escolher quem pode usar (Todos ou Usuários selecionados)  
  Definir número de métodos de autenticação (1 ou 2) → Ativar  
  Configurar métodos (e-mail, telefone, app autenticador, perguntas de segurança)  
  Exigir registro no SSPR (igual ao MFA)  
  Acessar relatórios para monitorar uso  

- Obs: O usuário deve responder entre 3 a 5 perguntas no registro. Na redefinição, ele precisa acertar a quantidade exigida pela política (ex: registrar 5, responder 3).

---

## 7. "Usage Location" (Local de Uso)
- País onde o usuário utilizará os serviços Microsoft.
- Obrigatório para atribuição de licenças (ex: Microsoft 365).
- Garante conformidade legal garantindo que leis locais de privacidade e proteção de dados (ex: LGPD, GDPR) sejam respeitadas.

---

## 8. Recursos-Chave de Gerenciamento de Identidade
- Gerenciamento de usuários, grupos e dispositivos
- Políticas de acesso condicional
- MFA
- SSPR
- Sincronização com AD local (Azure AD Connect)
- Logs e relatórios

---

## 9. Tipos de Integração de Dispositivos

| Tipo                  | Descrição                              |
|-----------------------|--------------------------------------|
| Ingressar no Azure AD  | Dispositivos corporativos, login organizacional |
| Registrar no Azure AD  | Dispositivos pessoais (BYOD), acesso limitado |
| Conectar ao Azure AD   | Integra AD local e Entra ID (modo híbrido) |
| Habilitar dispositivo  | Ativa um dispositivo já registrado   |

---

## 10. Sincronização com Ambiente Local

| Elemento      | Ferramenta Recomendada   |
|---------------|-------------------------|
| Usuários e Grupos | Azure AD Connect         |
| Banco de Dados    | Azure SQL Data Sync      |
| Arquivos          | Azure File Sync          |

---

## 11. Colaboração Externa (B2B) - Azure Active Directory
- "Invite External User" = Convidar usuário externo
- Funcionalidade: Compartilhar acesso a Teams, SharePoint, etc.
- Acesso com conta pessoal/corporativa
- Controle via políticas, grupos e roles

---

## 12. Autenticação vs Autorização

| Conceito      | Definição                       |
|---------------|--------------------------------|
| Autenticação  | Verifica quem é o usuário (login) |
| Autorização   | Define o que ele pode acessar/fazer |

---

## 13. Papéis Administrativos no Entra ID

| Função              | Permissões                                   |
|---------------------|----------------------------------------------|
| Administrador Global | Acesso total                                 |
| Administrador de Usuários | Criar/editar/excluir usuários, redefinir senhas |

---

## 14. Perfil do Usuário
- Informações como foto, cargo e telefone são opcionais, mas úteis para organização.
- Não são obrigatórias na criação da conta.

---

## 15. Logs no Entra ID

| Tipo de Log    | Informações                                       |
|----------------|--------------------------------------------------|
| Sign-in Logs   | Tentativas de login, local, IP, sucesso ou falha |
| Audit Logs     | Ações administrativas (criação, exclusão, alteração) |

---

## 16. Criação e Exclusão em Massa de Usuários
- Permissões necessárias: Administrador Global ou Administrador de Usuários.
- Para criar usuários em um tenant do Microsoft Entra ID, a pessoa precisa ter um papel administrativo adequado, como Administrador Global ou Administrador de Usuário. Caso contrário, mesmo que o tenant tenha sido criado, ela não terá essa permissão imediatamente.

✅ **Criação em massa via CSV**  
Caminho:  
Portal Microsoft Entra → Usuários → Todos os usuários → Criar usuário → Criação em massa → Baixar e preencher o modelo CSV.  
O modelo inclui colunas como: UserPrincipalName, DisplayName, FirstName, LastName, UsageLocation, etc.  

Após preencher o modelo, envie o arquivo pelo portal.

❌ **Exclusão em massa via CSV**  
Caminho:  
Portal Microsoft Entra → Usuários → Todos os usuários → Excluir usuários em massa → Baixar modelo CSV → Preencher com os UserPrincipalName dos usuários a serem removidos → Enviar o arquivo.  
⚠️ A exclusão é lógica: os usuários excluídos vão para a lixeira e podem ser restaurados em até 30 dias.  
📅 Exemplo: Excluído em 13/06, pode ser restaurado até 12/07.

---

## 17. Grupos no Entra ID

| Tipo              | Finalidade                           |
|-------------------|------------------------------------|
| Grupo de Segurança | Controle de acesso a apps, arquivos|
| Grupo Microsoft 365| Colaboração (Teams, Outlook, SharePoint)|

| Recurso          | Segurança | Microsoft 365 |
|------------------|-----------|--------------|
| Suporta usuários | ✅        | ✅           |
| Suporta dispositivos | ✅     | ❌           |
| Atribuição dinâmica | ✅ (usuário/dispositivo) | ✅ (usuário) |
| Gera e-mail e SharePoint | ❌   | ✅           |

---

## 18. Tipos de Atribuição

| Tipo             | Descrição                              |
|------------------|--------------------------------------|
| Atribuído        | Adição manual de membros              |
| Usuário Dinâmico | Adição automática com base em regras (ex: Departamento = RH) |
| Dispositivo Dinâmico | Somente em grupo de segurança      |

---

## 19. Atribuição de Licenças
- Licenças gratuitas: oferecem SSO (logon único) e gerenciamento básico de usuários.
- Licenças P1/P2: incluem recursos avançados como acesso condicional, SSPR (redefinição de senha), PIM (gerenciamento de privilégios).
- Microsoft 365: licenças atribuídas por usuário, não são compartilháveis.
- Como verificar licenças disponíveis:  
  No portal Microsoft Entra ID, vá em Licenças → Todos os produtos para visualizar o total de licenças adquiridas, atribuídas e disponíveis.

---

## 20. Gestão de Licenças – Ações

| Ação            | Descrição                              |
|-----------------|--------------------------------------|
| Ver planos      | Ver licenças disponíveis              |
| Definir local de uso | Obrigatório para atribuição       |
| Atribuir/remover | Manual ou por grupo                   |
| Modificar planos | Ativar/desativar recursos            |
| Remover licença | Libera para outro usuário             |

---

## 21. Unidades Administrativas (UA)
- Permitem delegar permissões administrativas segmentadas por setor, região ou departamento.  
- Exemplo: O gerente de TI da filial do Rio de Janeiro pode gerenciar apenas os usuários dessa localidade, sem acesso ao restante do tenant.  
- Requisitos: Licença Microsoft Entra ID P1 ou P2, ou Ser Administrador Global.

**Como criar uma Unidade Administrativa:**  
Portal Microsoft Entra → Unidades Administrativas → + Nova unidade administrativa → Informar nome e, se desejar, uma descrição → Criar.

**Como adicionar usuários ou grupos:**  
Acesse a UA criada → Aba Membros → + Adicionar membro → Selecione os usuários ou grupos desejados → Selecionar.

**Como delegar funções administrativas:**  
Acesse a UA → Aba Atribuições de função → + Adicionar atribuição → Escolha a função (ex: Administrador de usuários) → Selecione o usuário ou grupo → Confirmar.

---

## 22. Sincronização com AD Local
- Com Azure AD Connect, a sincronização é:
  - Do local para a nuvem: ✅
  - Da nuvem para o local: ❌ (exceto em configurações especiais)

---

## 23. Verificação de Domínio (registro TXT)
- Usado para provar que você é dono do domínio (ex: empresa.com.br).

### Como essa verificação é feita?
- A Microsoft pede para você criar um registro TXT no painel de DNS do seu domínio.  
- Esse registro não muda nada visível, serve só como um "selo de posse".

### Exemplo do Registro TXT

| Campo     | Valor Exemplo     | Explicação                               |
|-----------|-------------------|-----------------------------------------|
| Tipo      | TXT               | É um tipo de registro de texto no DNS   |
| Nome/Host | @                 | Representa o domínio raiz                |
| Valor/Destino | MS=ms35436768  | Código fornecido pela Microsoft          |
| TTL       | 3600              | Tempo de cache (em segundos)             |

⚠️ Configure no DNS do seu provedor (ex: Registro.br, GoDaddy, Cloudflare).

---

## 24. Perguntas-Chave de Prova (Exemplos)

| Pergunta                        | Resposta Correta          |
|--------------------------------|--------------------------|
| Como delegar administração por setor? | Unidade Administrativa      |
| Como adicionar usuário externo?        | Convidado (B2B)            |
| Função com acesso total?                | Administrador Global       |
| Como criar usuários em massa?           | Upload de CSV              |
| Usuário criado na nuvem replica para o AD local? | ❌ Não                     |
| Função com quase tudo, exceto papéis?   | Contribuinte               |
| O que ocorre ao excluir conta?           | Pode ser restaurada por 30 dias |
| Diferença: grupo de segurança × M365?    | Segurança = controle; M365 = colaboração |

---

## Referências

- https://learn.microsoft.com/pt-br/azure/active-directory/fundamentals/  
- https://mslabs.cloudguides.com/guides/AZ-104%20Exam%20Guide%20-%20Microsoft%20Azure%20Administrator%20Exercise%201/

 
