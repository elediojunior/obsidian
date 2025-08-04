---
{"dg-publish":true,"permalink":"/implantacao-do-controle-de-condicionantes/","noteIcon":""}
---

### Escopo
Cadastro
- Nomes
- Status
	- Não iniciada / Em andamento / Cumprida / Atrasada
- Tipo
	- Ambiental / Estrutural / Industrial / Manutenção
- [x] Responsáveis
- Prazo
	- Sem prazo / Data fixa / Recorrente
- Notificações?
- Anexos
- Checklist

### Devz
- [x] Opção de manter o anexo atual
- [ ] Historical

Pós migration:
- [x] Executar queries de permissão:
      INSERT INTO RoleClaims (RoleId,ClaimType,ClaimValue) SELECT RoleId,'PermissionLevelDocumentCondition',ClaimValue FROM RoleClaims WHERE ClaimType='PermissionLevelDocumentCost';
      INSERT INTO RoleClaims (RoleId,ClaimType,ClaimValue) SELECT RoleId,'PermissionLevelDocumentConditionType',ClaimValue FROM RoleClaims WHERE ClaimType='PermissionLevelCostType';
- [x] Atualizar permissionamentos
      update RoleClaims set ClaimType='PermissionLevelCondition' where ClaimType='PermissionLevelDocumentCondition';
      update RoleClaims set ClaimType='PermissionLevelConditionType' where ClaimType='PermissionLevelDocumentConditionType';
