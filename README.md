# Solicitações à Secretaria de Obras e Infraestrutura – Pindaí/BA

Sistema para o morador de Pindaí pedir serviços à Secretaria Municipal de Obras e Infraestrutura pelo celular, sem instalar aplicativo, e para a equipe da Secretaria atender cada pedido e registrar o serviço com foto, data e hora.

## Visão geral

| Parte | Quem usa | O que faz |
|---|---|---|
| `index.html` | Morador | Formulário público com mapa, GPS, foto e telefone. Gera o número de protocolo e permite consultar o andamento. |
| `painel.html` | Equipe da Secretaria | Painel com login por código. Cada equipe vê só os pedidos do seu tipo, inicia o atendimento e marca como atendido com foto. |
| `Code.gs` | (interno) | Script do Google Apps Script: grava na planilha, controla o acesso, guarda as fotos no Drive e mantém o histórico. |
| Planilha | Secretário, Triagem | Banco de dados organizado e protegido, com aba de resumo (gráficos). |

Tipos de pedido: água boa (potável), água não tratada, iluminação pública e reparo de estradas.

## A planilha

| Aba | Conteúdo | Quem edita |
|---|---|---|
| **Painel** | Resumo com totais, gráficos, tempo médio de atendimento e pedidos atrasados. Atualiza sozinha. | Ninguém (só leitura) |
| **Pedidos** | Todos os pedidos. Colunas amarelas (**Status** e **Observações da Secretaria**) são liberadas; as demais são protegidas. As colunas cinza (início e conclusão do atendimento) são preenchidas pelo painel. | Só as colunas amarelas |
| **Equipe** | Nome, perfil, código de acesso e se está ativo. | Somente o dono da planilha |
| **Histórico** | Registro de cada ação (quem, quando, de qual situação para qual). | Ninguém (só leitura) |

Situações: Recebido, Em análise, Em atendimento, Atendido e Não procede.

## Quem acessa o quê

| Perfil | Vê | Pode fazer |
|---|---|---|
| Secretário | Todos os tipos e o resumo | Tudo, inclusive reabrir pedidos |
| Triagem | Todos os tipos e o resumo | Colocar em análise, iniciar, atender e marcar "Não procede" (com motivo) |
| Água | Água boa e água não tratada | Iniciar e marcar como atendido (foto obrigatória) |
| Iluminação | Iluminação pública | Iniciar e marcar como atendido (foto obrigatória) |
| Estradas | Estradas | Iniciar e marcar como atendido (foto obrigatória) |

Ao marcar como atendido, ficam gravados: data e hora, nome de quem atendeu, foto do serviço, observação e, se o aparelho permitir, a localização de onde o serviço foi feito.

## Instalação

### 1. Script

1. Na planilha, abra **Extensões > Apps Script**, apague o código e cole o `Code.gs`. Salve.
2. Escolha a função **configurarPlanilha** e clique em **Executar**. Autorize quando o Google pedir. Ela cria as abas, as proteções e o gatilho de registro.
3. Na aba **Equipe**, preencha **Nome** e **Perfil** de cada pessoa. No menu **Solicitações**, clique em **Gerar códigos que estão em branco**.
4. Publique: **Implantar > Gerenciar implantações > lápis > Nova versão > Implantar**. Confirme "Executar como: Eu" e "Quem pode acessar: Qualquer pessoa". A URL `/exec` continua a mesma.

### 2. Site

1. Envie `index.html`, `painel.html` e `README.md` ao repositório do GitHub.
2. Confira que a linha `APPS_SCRIPT_URL` (no `index.html`) e `API` (no `painel.html`) têm a URL `/exec` do seu script.
3. O formulário fica em `.../index.html` (o endereço principal) e o painel em `.../painel.html`.

### 3. Compartilhar a planilha

- **Triagem:** compartilhe como **Editor**. As proteções limitam a edição às colunas Status e Observações.
- **Secretário:** compartilhe como **Leitor** (ou como Editor, se ele também for administrar a aba Equipe; nesse caso adicione-o como editor nas proteções da planilha).
- **Equipes de campo (Água, Iluminação, Estradas):** **não compartilhe a planilha**. Elas usam só o painel, com o código.
- **Pasta de fotos no Drive:** se a Triagem precisar abrir as fotos direto da planilha, compartilhe a pasta com ela como Leitora. No painel as fotos aparecem sem isso.

## Segurança e LGPD

- O compartilhamento do Google Planilhas não separa colunas por pessoa: quem abre a planilha vê todos os dados, inclusive telefones. Por isso as equipes de campo usam o painel, que entrega só os pedidos do tipo delas.
- O código de acesso é pessoal. Para bloquear alguém, escreva **Não** na coluna **Ativo** da aba Equipe. Depois de muitas tentativas erradas, o login é travado por 10 minutos.
- O painel é para uso interno e não é indexado por buscadores, mas o endereço não é secreto: a proteção é o código.
- A consulta pública de protocolo mostra apenas tipo, data e situação, sem dados pessoais.
- Defina com a Prefeitura por quanto tempo os dados e as fotos serão guardados.

## Personalização

No `Code.gs`: `CONFIG.DIAS_ALERTA` (dias para um pedido aparecer como atrasado), `CONFIG.EMAIL_AVISO` (aviso por e-mail a cada pedido novo) e `PERFIS` (quais tipos cada equipe enxerga).
No `index.html`: comunidades sugeridas, tipos e opções de problema, posição inicial do mapa.

## Tecnologias

HTML, CSS e JavaScript puros, mapa com [Leaflet](https://leafletjs.com/), mapa base do OpenStreetMap e imagens de satélite da Esri, Google Apps Script, Google Planilhas e Google Drive.

## Limitações

- Precisa de internet no momento do envio e do atendimento.
- O login por código é mais simples que uma conta individual. Se a Prefeitura adotar Google Workspace institucional, é possível migrar para login por conta.
- Alterações feitas direto na coluna Status da planilha são registradas no Histórico, mas sem foto. O atendimento com foto é feito pelo painel.

## Contato

Secretaria Municipal de Obras e Infraestrutura
Prefeitura Municipal de Pindaí
Parque Velho Tico, s/n, Alvorada, CEP 46360-000, Pindaí-BA
