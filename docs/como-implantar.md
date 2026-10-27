# Como implantar

## Pré-requisitos

- Microsoft 365 com Power Apps e Power Automate (licença padrão do M365 é suficiente — todos os conectores são *Standard*).
- Permissão para criar um site no SharePoint (ou usar um existente).
- Acesso a um ambiente do Power Platform onde você possa importar soluções.

## 1. SharePoint

1. Crie um site, por exemplo `https://<seu-tenant>.sharepoint.com/sites/AvaliacaoColaboradores`.
2. Crie as 9 listas com as colunas descritas em [`estrutura-dados.md`](estrutura-dados.md). Use exatamente os nomes internos das colunas.
3. Na lista **StatusAvaliacoes**, cadastre as etapas 10, 20, 30, 40 e 50.
4. Preencha **BaseCargos**, **BaseDptos** e **BaseColaboradores** com os dados da empresa (o e-mail do colaborador precisa ser o mesmo da conta Microsoft 365, porque o app identifica o usuário pelo login).

> Se preferir, as listas de cadastro podem ficar em outro site (por exemplo, um site de RH já existente) — use a variável `lf_SiteBase` para apontar para ele.

## 2. Importar a solução

1. Acesse [make.powerapps.com](https://make.powerapps.com) e selecione o ambiente.
2. **Soluções → Importar solução** e escolha `solution/AvaliacaoColaboradores_1_0_0_2_managed.zip`.
3. Em **Conexões**, crie ou selecione uma conexão para:
   - SharePoint (`lf_SharePoint`)
   - Office 365 Outlook (`lf_OutlookOffice`)
   - Usuários do Office 365 (`lf_Office365Users`)
4. Em **Variáveis de ambiente**, informe o site e selecione cada lista criada no passo 1.
5. Conclua a importação.

## 3. Pós-importação

1. Abra a solução e confirme que os fluxos `[Avaliação Colaboradores] - Convite Email` e `[Avaliação Colaboradores] - Excluindo Base Avaliação` estão **ativados**.
2. Compartilhe o app com os usuários (ou com um grupo de segurança) e dê a eles permissão de edição nas listas do SharePoint.
3. **Restrinja o acesso à área de administração.** Nesta versão, o botão que leva à tela **Admin** (`Image6_31`, na Home) e o seletor de teste `tg_FalsoStart` ficam visíveis para todos. Antes de liberar para os usuários, defina a propriedade `Visible` deles com a sua regra de administradores, por exemplo:
   ```
   User().Email in ["rh@suaempresa.com", "admin@suaempresa.com"]
   ```
   Para uma regra mais robusta, use uma lista de administradores no SharePoint ou um grupo do Microsoft 365. Lembre também que a segurança real está nas **permissões das listas do SharePoint** — esconder um botão não impede o acesso aos dados.

## 4. Primeiro ciclo

1. Na tela **Admin**, crie uma avaliação com nome, período e datas.
2. Cadastre os itens (competências) da avaliação.
3. Selecione os colaboradores participantes e envie os convites.
4. Acompanhe o status de cada colaborador pela própria tela de administração.

## Personalização

- **Cores**: altere `CoresLight` / `TextCoresLight` em `App.Formulas`.
- **Escala de notas**: altere a coleção `colRespostasMetas` em `App.OnStart`.
- **Texto do convite**: edite a ação *Enviar um email (V2)* do fluxo de convite.
