---
{"dg-publish":true,"permalink":"/power-bi-rd/","noteIcon":""}
---

Critérios de Classificação. Alteração dos critérios e parametrização no sistema (Dashboard)
##### REGULAR
 - Regular: Documento emitido e vigente.
 - Em andamento: Processo de renovação com protocolo válido.
##### EM ANDAMENTO
 - Atrasado: Documento fora da vigência, mas com processo iniciado mas sem protocolo.
##### IRREGULAR
- Vencido ou Inexistente sem processo criado.

Inviável tecnicamente: Regularização impedida por terceiros (ex.: locador). Verificar a possibilidade de colocar alguma etiqueta que identifique o motivo da irregularidade “tecnicamente ou financeiramente”.
Inviável financeiramente: Custo-benefício não justifica a regularização.

Quais Docs: 5 licenças (funcionamento, sanitária, avcb, ambiental, habite-se).

![Pasted image 20250802231646.png](/img/user/Attachments/2023/Pasted%20image%2020250802231646.png)

![Pasted image 20250802231700.png](/img/user/Attachments/2023/Pasted%20image%2020250802231700.png)

Planilha enviada pela Lara
![[racional meta rd.xlsx]]

Relatório X9:

![Pasted image 20250802231753.png](/img/user/Attachments/2023/Pasted%20image%2020250802231753.png)

### Regras vigentes
```
// Em andamento
    DocumentsDetails[DocumentStatusName] = "Inexistente/Em obtenção" &&
    DocumentsDetails[StatusProtocolName] = "Sem protocolo", "Em andamento",

DocumentsDetails[DocumentStatusName] = "Vencido/Em renovação" &&
DocumentsDetails[StatusProtocolName] = "Sem protocolo", "Em andamento",

// Irregular
DocumentsDetails[DocumentStatusName] IN { "Inexistente", "Vencido", "Não configurado" }, "Irregular",

// Regular
DocumentsDetails[DocumentStatusName] = "Inexistente/Em obtenção" &&
DocumentsDetails[StatusProtocolName] <> "Sem protocolo", "Regular",

DocumentsDetails[DocumentStatusName] = "Vencido/Em renovação" &&
(
	ISBLANK(DocumentsDetails[StatusProtocolName]) ||
	DocumentsDetails[StatusProtocolName] <> "Sem protocolo"
), "Regular",

DocumentsDetails[DocumentStatusName] IN {
	"Vigente",
	"Permanente",
	"Isento",
	"Vigente/Em renovação"
}, "Regular"
```
