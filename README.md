Solicitações à Secretaria de Obras e Infraestrutura – Pindaí/BA

Formulário web para o morador de Pindaí pedir serviços à Secretaria Municipal de Obras e Infraestrutura pelo celular, sem instalar aplicativo. Os pedidos caem numa planilha do Google, já organizados por tipo, comunidade e situação.

O que o morador consegue pedir
Água boa (potável)
Água não tratada
Iluminação pública (troca de ponto, lâmpada queimada, poste danificado)
Reparo de estradas
Como funciona para o morador
Escolhe o tipo de solicitação e o problema.
Marca o local no mapa: pelo botão "Estou no local agora" (GPS do celular) ou tocando no ponto do pedido. O pino pode ser arrastado para ajustar.
Informa a comunidade, um ponto de referência, o nome e o telefone com DDD.
Pode anexar uma foto e escrever uma descrição.
Ao enviar, recebe um número de protocolo (exemplo: PIN-2026-00001) e pode acompanhar a situação do pedido na própria página.
Como funciona para a Secretaria

Cada pedido vira uma linha na aba Pedidos da planilha, com:

protocolo, data e hora, tipo, problema, comunidade e ponto de referência;
nome, telefone e se tem WhatsApp;
latitude, longitude e link "Abrir mapa" (Google Maps);
como o local foi marcado (GPS do celular ou mapa) e a precisão do GPS;
link da foto, guardada numa pasta do Google Drive;
Status, que a equipe atualiza: Recebido, Em análise, Em atendimento, Concluído ou Não procede;
coluna de observações da Secretaria.
Arquivos
Arquivo	Função
index.html	Página do formulário (mapa, GPS, foto, consulta de protocolo). Roda direto no navegador.
Code.gs	Script do Google Apps Script que recebe os pedidos, gera o protocolo, grava na planilha e salva as fotos no Drive.
Instalação
1. Planilha e script
Crie uma planilha no Google Planilhas.
Abra Extensões > Apps Script, apague o conteúdo e cole o Code.gs.
Clique em Implantar > Nova implantação > App da Web:
Executar como: Eu
Quem pode acessar: Qualquer pessoa
Autorize o acesso à planilha e ao Drive quando o Google pedir.
Copie a URL que termina em /exec.
2. Formulário
No index.html, localize a linha APPS_SCRIPT_URL e cole a URL do passo anterior.
Publique o index.html em um endereço HTTPS (por exemplo GitHub Pages, Netlify ou o site da Prefeitura). O GPS do celular só funciona em HTTPS.
Gere um QR Code do endereço para cartazes e grupos de WhatsApp das comunidades.
3. Publicando no GitHub Pages
Crie um repositório e envie o index.html e este README.md (o Code.gs também pode ir, já que não contém dados pessoais).
Em Settings > Pages, escolha a branch principal e a pasta raiz.
O endereço será https://SEU-USUARIO.github.io/NOME-DO-REPOSITORIO/.
Personalização

No começo do script do index.html:

APPS_SCRIPT_URL: endereço do Apps Script.
CENTRO e ZOOM_CIDADE: posição inicial do mapa.
COMUNIDADES: sugestões que aparecem no campo de comunidade.
TIPOS: tipos de solicitação e as opções de problema de cada um.

No começo do Code.gs:

CONFIG.EMAIL_AVISO: e-mail que recebe um aviso a cada pedido novo (opcional).
CONFIG.PREFIXO: prefixo do número de protocolo.
TIPOS_VALIDOS: precisa ter os mesmos nomes de tipo usados no index.html.

Depois de alterar o Code.gs, use Implantar > Gerenciar implantações > Nova versão. A URL continua a mesma.

Privacidade (LGPD)
O formulário coleta nome, telefone e localização e pede a concordância do morador antes do envio.
Os dados são usados apenas para atender a solicitação.
Mantenha a planilha e a pasta de fotos compartilhadas somente com a equipe da Secretaria.
A consulta pública de protocolo devolve apenas tipo, data e situação, sem dados pessoais.
Defina com a Prefeitura por quanto tempo os dados serão guardados.
Tecnologias

HTML, CSS e JavaScript puros, mapa com Leaflet, mapa base do OpenStreetMap e imagens de satélite da Esri, Google Apps Script, Google Planilhas e Google Drive.

Limitações
Precisa de internet no momento do envio. Em áreas sem sinal, o morador deve tentar de novo quando estiver com conexão, ou procurar a Secretaria presencialmente.
O mapa base do OpenStreetMap é adequado para o volume de uma cidade pequena. Se o uso crescer muito, considere um provedor de mapas próprio.
O envio de fotos é limitado pelo tamanho que o Apps Script aceita; o formulário já reduz as imagens automaticamente.
Contato

Secretaria Municipal de Obras e Infraestrutura Prefeitura Municipal de Pindaí Parque Velho Tico, s/n, Alvorada, CEP 46360-000, Pindaí-BA
