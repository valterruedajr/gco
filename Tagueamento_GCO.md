

# Documentação para Tagueamento do site de GCO


## Pontos de destaque


> Ao validar o tagueamento do site no último mês (maio), notamos algumas inconsistências e métodos utilizados que podem comprometer e descredenciar a coleta de dados. 

- DataLayer de purchase disparando apenas para o fluxo de compra da assinatura ilimitada, enquanto os outros fluxos têm um disparo de Purchase via GTM acionados por uma pageview.

- Também notamos disparos de eventos excessivos durante os possíveis fluxos de navegação do site.
  
- Mais de um FormSubmit sendo disparado quando não há preenchimento de formulário. 

- Listamos todos os disparos no link: [Tagueamento_GCO](https://docs.google.com/spreadsheets/d/1PVFOFw4z8Af9XDYtISadASGhbRDalczCh85s_dBsdLI/edit#gid=2054088160) na aba "DataLayer Atual"
  
- Nos fluxo de compra após o usuário ter interagido com os resultados de pesquisa notamos que o dataLayer addToCart não dispara, isso impossibilita o disparo de muitas tags.
  

>Inicialmente esse documento contempla apenas os dados de Google Analytics, após os devidos ajustes serem realizados, revisaremos todas as tags de mídia e outros serviços que estão inseridos no site.

>>Importante: Toda alteração no site, seja na identidade visual ou no código, deve ser informada para o time da Blinks com antecedência. Assim conseguimos evitar possíveis falhas ou erros no tagueamento e ter o tempo necessário para fazer as devidas validações. Não seguir essa orientação, pode Trazer consequências na coleta dos dados e principalmente no investimento aplicado nas plataformas de mídia, que por sua vez podem sofrer as consequências das modificações sem a devida validação.

Se tiverem dúvidas sobre a Planilha, podem encaminhar para gustavo.hamamoto@essenceglobal.com, leonardo.pimentel@essenceglobal.com e valter.junior@essenceglobal.com

&nbsp;

>## Coleta de Dados

Esse documento formaliza a coleta de dados do site [Institucional](https://www.grancursosonline.com.br/)  e todos os subdominios que estão abaixo, como: [Blog](https://blog.grancursosonline.com.br/); [Questões](https://questoes.grancursosonline.com.br/); [Pós](https://pos.grancursosonline.com.br/); [Concursos](https://concursos.grancursosonline.com.br) e possívelmente outros que entrarão no futuro.

Em primeiro momento será necessário inserir o Google Tag Manager, plataforma utilizada pelo time de BI da Blinks, para injetar scripts e configurar a coleta. A coleta sólida dos dados digitais tem como pré-requisito todas as atividades aqui listadas bem como as configurações a serem realizadas pelo time de BI da Blinks.
&nbsp;
>## Google Tag Manager - Setup
 
Faremos a coleta e envio das interações pelo Google Tag Manager. Para isso é necessária a implementação dos seguintes snippets em todas as páginas .
 
>Esse snippet do GTM deve ser inserido no domínio e nos subdomínios do site. A ideia é centralizar todos os dados em uma mesma propriedade do Google Analytics evitando assim o uso do crossdomain. 

>>Vale reforçar que como os fluxos dos subdomínios apontam para o domínio principal, essa prática seria a ideia. Outro ponto, podemos criar vistas distintas para cada subdomínio de Gran Cursos Online.
 
O primeiro, deve ser implementado na tag <head> do html, o mais alto possível:

```
Paste this code as high in the <head> of the page as possible:
 
<!-- Google Tag Manager -->
<script>(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start':
new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0],
j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src=
'https://www.googletagmanager.com/gtm.js?id='+i+dl;f.parentNode.insertBefore(j,f);
})(window,document,'script','dataLayer','GTM-NP5DCX');</script>
<!-- End Google Tag Manager -->
```

```
Additionally, paste this code immediately after the opening <body> tag:
 
<!-- Google Tag Manager (noscript) -->
<noscript><iframe src='https://www.googletagmanager.com/ns.html?id=GTM-NP5DCX'
height='0' width='0' style='display:none;visibility:hidden'></iframe></noscript>
<!-- End Google Tag Manager (noscript) -->
```
 
>>Adendo de Enhanced Ecommerce Para algumas páginas será necessária a inicialização de uma variável de dataLayer contendo dados sobre a página que deve ser inserida antes ainda dos snippets citados acima.

 &nbsp;
>## Disparos
 
É responsabilidade dos desenvolvedores do site configurar a chamada e a disponibilização dos dados solicitados abaixo.

Configurar os seguintes pushs na variável global dataLayer nos momentos listados abaixo com a estrutura informada.

>>## Atenção
>>Valores entre chaves ``{{valor}}`` são informações que devem ser preenchidas dinamicamente através da escolha do usuário.

&nbsp;
>### Datalayers (interações)
<em>
Uma sugestão, inclusive, seria a de criar uma nova vista, considerando a nova estrutura de informação dos eventos e nomear a atual como OLD para manter o histórico.
</em>

Abaixo a documentação completa, contemplando os eventos mais relevantes de interação do site (incluindo correções na estrutura das dataLayer):

># Globais
&nbsp;
>### Download de materiais

Disparar imediatamente após o sucesso ou a falha no download de algum material no site. Blog, Materiais gratuitos etc.
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Identificação - Login',
 'eventAction': 'Ambiente: {{nome-do-ambiente}}', // Trazer o ambiente que o usuário está baixando o material. Ex: Blog, Material grátis, etc.
 'eventLabel': 'Status Download: {{nome-do-status}} - Material: {{nome-do-material}}' //Trazer o status do usuário, se teve sucesso ao baixar o material ou não e o nome do material.
});
```
&nbsp;
>### Banners (todos os banner do site - dominio principal e subdominios)

Disparar imediatamente após o clique no banner (em todos os banners do site, inclusive slider)
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Banners',
 'eventAction': 'Ambiente: {{nome-do-ambiente}}', 
 'eventLabel': 'Banner: {{nome-do-botao-ou-açao}}' //Trazer o nome do botão ou ação. Ex: Concursos, Home, etc.e Trazer o nome do botão
});
```
&nbsp;
>### Sucesso ou Falha em logar em todos os ambientes do site

Disparar imediatamente após o sucesso ou a falha no login. Em todos os ambientes.
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Identificação - Login',
 'eventAction': 'Ambiente: {{nome-do-ambiente}}', // Trazer o ambiente que o usuário está logando. Ex: Área do Aluno, Compra, Etc.
 'eventLabel': 'Status Login: {{nome-do-status}}' //Trazer o status do usuário, se teve sucesso ao logar ou não
});
```
&nbsp;
>### Sucesso ou Falha no cadastro

Disparar imediatamente após o sucesso ou a falha em cadastros (formulários). Em todos os formulários!
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Identificação - Cadastro',
 'eventAction': 'Cadastro: {{nome-do-formulario}} - Ambiente: {{nome-do-ambiente}} ', // Trazer tipo de formulário que o usuário está preenchendo e o ambiente. Ex: Cadastro inicial para compra, Cadastro em eventos, Baixar material, Newsletter etc. Ambiente: Assinatura Ilimitada, Concurso etc.
 'eventLabel': 'Status Cadastro: {{nome-do-status}}' //Trazer o status do usuário, se teve sucesso ao cadastrar ou não
});
```
&nbsp;
>### Checkout (Botões no checkout)

Disparar imediatamente após o clique nos botões presentes no checkout (Confirmar compra, Imprimir Boleto, Finalizar compra, Voltar, Visualizar boleto )
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Checkout',
 'eventAction': 'Ambiente: {{nome-do-ambiente}}', //trazer o nome do fluxo. Ex: Concursos (+OAB, Redação e Pós), Assinatura ilimitada, Coaching e Questões
 'eventLabel': 'Botão: {{nome-do-botao}}' //Trazer o nome do botão. Ex: Confirmar Compra, Imprimir boleto, Finalizar compra, Voltar, Visualizar boleto
});
```
&nbsp;
># Institucional
&nbsp;

>### Institucional - Cabeçalho - Campo de Pesquisa

Disparar imediatamente após o usuário pesquisar algo
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Institucional',
 'eventAction': 'Cabeçalho',
 'eventLabel': 'Termo pesquisado: {{termo-pesquisado}}' //trazer o termo pesquisado
});
```
<em>Obs: Notamos que o acompanhamento de pesquisas não está configurado na vista principal do Google Analytics. Podemos fazer essa configuração?
</em>

&nbsp;
>### Institucional - Cabeçalho - Menu - Opção selecionada

Disparar imediatamente após o clique nas opções do menu: Carrinho, Vendas, Área do Aluno, Entrar e Assinatura limitada, Cursos, Questões, Pós-Graduação, Blog, Material grátis etc.
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Institucional',
 'eventAction': 'Cabeçalho',
 'eventLabel': 'Botão: {{opção-menu-clicada}}' //Trazer opção de menu clicada pelo usuário. Ex: Carrinho, Vendas, Área do Aluno, Entrar e Assinatura limitada, Cursos, Questões, Pós-Graduação, Blog, Material grátis etc.
});
```
&nbsp;
>### Institucional - Cabeçalho - Menu - Concurso - Opção selecionada

Disparar imediatamente após o clique na opção do menu cursos e clicou em um dos botões/links no submenu: Assinatura Ilimitada, CFC, Residência, Assinatura Ilimitada - 1 ano de acesso, Policia Federal etc.
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Institucional',
 'eventAction': 'Cabeçalho',
 'eventLabel': 'Menu: {{opção-menu-clicada}} - Link: {{nome-do-curso-ou-concurso}}' //Trazer opção de menu clicada pelo usuário Ex: Assinatura Ilimitada, CFC, Residência, Assinatura Ilimitada - 1 ano de acesso, Policia Federal etc.
});
```
&nbsp;
>### Institucional - Botão CTA - Interesse 

Disparar imediatamente após o clique nos botões de interesse: Ver todos os aulões, Ver todas as noticias, Ver todas as materias, Ver todos os concursos, Veja mais, Ver mais depoimentos e interação com os links e botoes disponiveis na home.
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Institucional',
 'eventAction': 'Botão CTA - Interesse',
 'eventLabel': 'Botão: {{nome-do-botao}}'         //Trazer o nome do botão. Ex: Ver todos os aulões, Ver todas as noticias, Ver todas as materias, Ver todos os concursos, Ver mais depoimentos e interação com os links e botoes disponiveis na home.
});
```
&nbsp;
>### Institucional - Rodapé Links

Disparar imediatamente após o clique nos links do rodapé: Quem somos, Central de Ajusta, Atendimento Online, Redes sociais etc.
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Institucional',
 'eventAction': 'Rodapé', 
 'eventLabel': 'Link: {{nome-do-link}}' //Trazer o nome do link. Ex: Quem somos, Central de Ajusta, Atendimento Online, Redes sociais etc.
});
```
&nbsp;
>### Institucional - Rodapé CTA

Disparar imediatamente após o clique nos CTAs do rodapé: Atendimento de vendas, Foi aprovado?
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Institucional',
 'eventAction': 'Rodapé', 
 'eventLabel': 'CTA: {{nome-do-cta}}' //Trazer o nome do botão. Ex: Atendimento de vendas, Foi aprovado?
});
```
&nbsp;
># Institucional - Concursos
&nbsp;

>### Institucional - Concursos - Botão CTA - Interesse

Disparar imediatamente após o clique nos botões de interesse. Ex: Baixar Edital, Saiba mais, Compartilhar, Pacotes, Cursos por materia, Todos os cursos
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Institucional - Concursos',
 'eventAction': 'Botão CTA - Interesse',
 'eventLabel': 'Botão: {{nome-do-botão}} - Ambiente: {{nome-do-ambiente}}'         //Trazer o nome do produto escolhido e ambiente. Ex produto: Baixar Edital, Saiba mais. Ex: ambiente: Pacvotes, Cursos por materia ou todos os cursos
});
```
&nbsp;
>### Institucional - Concursos - Botão CTA - Ação

Disparar imediatamente após o clique nos botões de visualizar (PDF) ou assistir (aula) PDF ou comprar o curso. Ex: Visualizar ou Assitir, Comprar
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Institucional - Concursos',
 'eventAction': 'Botão CTA - Ação',
 'eventLabel': 'Botão: {{nome-do-botão}} - Curso: {{nome-do-curso-ou-concurso}}'         //Trazer o nome do botão e o ambiente. Ex botão: Visualizar ou Assitir. Ex: curso: PC RN - Polícia Civil do Estado do Rio Grande do Norte - Agente e Escrivão de Polícia Civil Substituto - Treinamento Intensivo + Simulados
});
```
&nbsp;
># Institucional - Assinatura Ilimitada
&nbsp;
>### Institucional - Assinatura Ilimitada - Botão CTA - Interesse

Disparar imediatamente após o clique em botões do interesse. Ex: Teste por 30 dias, Chat online, Atendimento pelo whastapp
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Institucional - Assinatura Ilimitada',
 'eventAction': 'Botão CTA - Interesse',
 'eventLabel': 'Botão: {{nome-do-botao}}'  //Trazer o nome do plano e o periodo escolhido. Ex: Individualo Social e Assinatura 1 ano
});
```

>### Institucional - Assinatura Ilimitada - Botão CTA - Ação

Disparar imediatamente após a seleção do plano (incluir periodo)
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Institucional - Assinatura Ilimitada',
 'eventAction': 'Botão CTA - Ação',
 'eventLabel': 'Plano: {{nome-do-plano}} - Período: {{periodo-da-assinatura}}'  //Trazer o nome do plano e o periodo escolhido. Ex: Individualo Social e Assinatura 1 ano
});
```
&nbsp;

># Institucional - Material grátis

&nbsp;

<em>
Obs: Para o preenchimento do formulario e sucesso/falha do download do material, deve-se considerar as dataLayers globais de download.
</em>

&nbsp;

>## Institucional - Material grátis - Botão CTA - Interesse (filtro digitado)

Disparar imediatamente após o usuário digitar algo no campo de busca na página de materiais. 
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Institucional - Material grátis',
 'eventAction': 'Botão CTA - Interesse',
 'eventLabel': 'Botão: Buscou material'         //
});
```
&nbsp;

>## Institucional - Material grátis - Botão CTA - Interesse (filtro selecionado)

Disparar imediatamente após o usuário selecionar um dos filtros no meno da esquerda. Ex: OAB, Magistratura, Juridica etc.
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Institucional - Material grátis',
 'eventAction': 'Botão CTA - Interesse',
 'eventLabel': 'Botão: Buscou material - Filtro: {{filtro-selecionado}}'         // Ex: OAB, Magistratura, Juridica etc.
});
```
&nbsp;

>## Institucional - Material grátis - Botão CTA - Interesse (outros botões)

Disparar imediatamente após o usuário digitar algo no campo de ver mais, chat etc.
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Institucional - Material grátis',
 'eventAction': 'Botão CTA - Interesse',
 'eventLabel': 'Botão: {{nome-do-botao}}'         //ver mais, chat etc.
});
```
&nbsp;

>## Institucional - Material grátis - Botão CTA - Ação (material selecionado)

Disparar imediatamente após o usuário selecionar um dos filtros no meno da esquerda. Ex: OAB, Magistratura, Juridica etc.
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Institucional - Material grátis',
 'eventAction': 'Botão CTA - Ação',
 'eventLabel': 'Botão: Selecionou material - Material: {{nome-do-material}}'         // Ex: OAB – Manual Gran
});
```
&nbsp;

>## Institucional - Material grátis - Botão CTA - Ação (botões página do material)

Disparar imediatamente após o clique em um dos botões nas páginas de materiais
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Institucional - Material grátis',
 'eventAction': 'Botão CTA - Ação',
 'eventLabel': 'Botão: {{nome-do-botao}} - Material: {{nome-do-material}} //Trazer o nome do botão na pagina. Ex: Quero assinatura ilimitada agora ou Cursos para OAB e o nome do material.
});
```

&nbsp;

># Institucional - Aula grátis
&nbsp;
>### Institucional - Aula grátis - Botão CTA - Interesse

Disparar imediatamente após o clique em botões do interesse. Ex: Data escolhida (Dia, mes, ano, semana), Anterior, Hoje, Proximo
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Institucional - Aula Grátis',
 'eventAction': 'Botão CTA - Interesse',
 'eventLabel': 'Data: {{data-escolhida}}'  //Trazer a data escolhida. Ex: Data escolhida (Dia, mes, ano, semana), Anterior, Hoje, Proximo
});
```
&nbsp;
>### Institucional - Aula grátis - Botão CTA - Ação

Disparar imediatamente após a seleção da data clicando no botão inscreva-se e trazer o nome da aula escolhida. Ex: Língua Portuguesa - Concurso CGU: O que estudar em cada matéria
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Institucional - Aula Grátis',
 'eventAction': 'Botão CTA - Ação',
 'eventLabel': 'Botão: {{nome-do-botão}} - Aula: {{aula-escolhida}}'  //Trazer o nome do botão e o nome da aula escolhida. Ex: Língua Portuguesa - Concurso CGU: O que estudar em cada matéria
});
```
&nbsp;
># Institucional - Aula ao vivo
&nbsp;
>### Institucional - Aula ao vivo - Campo pesquisa

Disparar imediatamente após o usuário pesquisar algo nas aulas ao vivo
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Institucional - Aula ao vivo',
 'eventAction': 'Cabeçalho',
 'eventLabel': 'Aula pesquisada: {{termo-pesquisado}}' //trazer o termo pesquisado
});
```
&nbsp;
>### Institucional - Aula ao vivo - Botão CTA - Interesse

Disparar imediatamente após o clique em botões do interesse: Aula ao vivo escolhida. Ex: Treinamento Intensivo BB Escriturário
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Institucional - Aula ao vivo',
 'eventAction': 'Botão CTA - Interesse',
 'eventLabel': 'Aula: {{aula-escolhida}}'  //Trazer a data escolhida. Ex: Treinamento Intensivo BB Escriturário
});
```
&nbsp;
># Institucional - Professor
&nbsp;
>### Institucional - Professor - Campo pesquisa

Disparar imediatamente após o usuário pesquisar algo nos professores
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Institucional - Professor',
 'eventAction': 'Cabeçalho',
 'eventLabel': 'Professor pesquisado: {{termo-pesquisado}}' //trazer o termo pesquisado
});
```
&nbsp;
>### Institucional - Professor - Botão CTA - Interesse

Disparar imediatamente após o clique em botões do interesse: Professor(a) escolhido(a). Ex: ALEXANDRE MEIRELLES
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Institucional - Professor',
 'eventAction': 'Botão CTA - Interesse',
 'eventLabel': 'Professor: {{professor-escolhido}}'  //Trazer o professor(a) escolhido(a). Ex: ALEXANDRE MEIRELLES
});
```
&nbsp;
>### Institucional - Professor - Botão CTA - Ação

Disparar imediatamente após o clique em botões de ação: Pnome do professor e o nome do curso escolhida. Ex: Comprar - Treinamento Intensivo para PM PR - Polícia Militar do Estado do Paraná - Cadete - ADMILSON COSTA
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Institucional - Professor',
 'eventAction': 'Botão CTA - Ação',
 'eventLabel': 'Botão: {{nome-do-botão}} - Professor {{nome-do-professor}} - Curso: {{aula-escolhida}}'  //Trazer o nome do botão, nome do professor e o nome do curso escolhida. Ex: Comprar - Treinamento Intensivo para PM PR - Polícia Militar do Estado do Paraná - Cadete - ADMILSON COSTA
});
```
&nbsp;
># Institucional - CFC
&nbsp;

>### Institucional - CFC - Botão CTA - Interesse

Disparar imediatamente após o clique nos botões de interesse (exclusivo para CFC, deve ser apartado de concursos). Ex: Baixar Edital, Saiba mais, Compartilhar, Pacotes, Cursos por materia, Todos os cursos
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Institucional - CFC',
 'eventAction': 'Botão CTA - Interesse',
 'eventLabel': 'Botão: {{nome-do-botão}} - Ambiente: {{nome-do-ambiente}}'         //Trazer o nome do produto escolhido e ambiente. Ex produto: Baixar Edital, Saiba mais. Ex: ambiente: Pacotes, Cursos por materia ou todos os cursos
});
```
&nbsp;
>### Institucional - CFC - Botão CTA - Ação

Disparar imediatamente após o clique nos botões de visualizar (PDF) ou assistir (aula) PDF ou comprar o curso. Ex: Visualizar ou Assitir, Comprar
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Institucional - CFC',
 'eventAction': 'Botão CTA - Ação',
 'eventLabel': 'Botão: {{nome-do-botão}} - Curso: {{nome-do-curso-ou-concurso}}'         //Trazer o nome do botão e o ambiente. Ex botão: Visualizar ou Assitir. Ex: curso: Exame de Suficiência CFC 2021.2 - Resumo + Questões + Simulados e Revisão Final
});
```
&nbsp;
># Institucional - Residência
&nbsp;
>### Institucional - Residência - Botão CTA - Interesse

Disparar imediatamente após o clique nos botões de interesse (exclusivo para Residência). Ex: Saiba mais, Pacotes, Cursos por materia, Carregar mais cursos
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Institucional - Residência',
 'eventAction': 'Botão CTA - Interesse',
 'eventLabel': 'Botão: {{nome-do-botão}} - Ambiente: {{nome-do-ambiente}}'         //Trazer o nome do produto escolhido e ambiente. Ex produto: Saiba mais. Ex: ambiente: Pacotes, Cursos por materia ou todos os cursos
});
```
&nbsp;
>### Institucional - Residência - Botão CTA - Ação

Disparar imediatamente após o clique nos botões de visualizar (PDF) ou assistir (aula) PDF ou comprar o curso. Ex: Visualizar ou Assitir, Comprar
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Institucional - Residência',
 'eventAction': 'Botão CTA - Ação',
 'eventLabel': 'Botão: {{nome-do-botão}} - Curso: {{nome-do-curso-ou-concurso}}'         //Trazer o nome do botão e o ambiente. Ex botão: Visualizar ou Assitir. Ex: curso: Exame de Suficiência CFC 2021.2 - Resumo + Questões + Simulados e Revisão Final
});
```
&nbsp;
># Institucional - Aprovados
&nbsp;

>### Institucional - Aprovados - Botão CTA - Interesse

Disparar imediatamente após o clique em botões do interesse: Veja todos os resultados
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Institucional - Aprovados',
 'eventAction': 'Botão CTA - Interesse',
 'eventLabel': 'Botão: {{nome-do-botão}} - Concurso: {{nome-do-concurso}}'  //Trazer o nome do botão. Ex: Veja todos os resultados
});
```
&nbsp;
># OAB
&nbsp;
>### OAB - Cabeçalho 

Disparar imediatamente após o clique nos botões do menu (Materiais Gratuitos, Blog)
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - OAB',
 'eventAction': 'Cabeçalho',
 'eventLabel': 'Botão: {{nome-do-botao}}'         //Trazer o nome do botão. Ex: Materiais Gratuitos, Blog e Entrar
});
```
&nbsp;

>### OAB - Botão CTA - Interesse 

Disparar imediatamente após o clique nos botões de interesse (Entrar, Faça o teste agora, Saiba mais)
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - OAB',
 'eventAction': 'Botão CTA - Interesse',
 'eventLabel': 'Botão: {{nome-do-botao}}'         //Trazer o nome do botão. Ex: Entrar, Faça o teste agora, Saiba mais)
});
```
&nbsp;
>### OAB - Botão CTA - Ação

Disparar imediatamente após o clique nos botões de ação (Estou pronto - Modal e Comprar)
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - OAB',
 'eventAction': 'Botão CTA - Ação',
 'eventLabel': 'Botão: {{nome-do-botao}}'         //Trazer o nome do botão. Ex: Estou pronto - Modal;
});
```
&nbsp;
>### OAB - Botão CTA - Ação - Comprar

Disparar imediatamente após o clique nos botões de ação Comprar no conteúdo (Comprar)
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - OAB',
 'eventAction': 'Botão CTA - Ação',
 'eventLabel': 'Botão: {{nome-do-botao}} - Fase: {{fase-escolhida-ou-coaching}}'       //Trazer o nome do botão e a fase (ou coaching). Ex: Comprar e Coaching
});
```
&nbsp;
>### OAB - Rodapé CTA

Disparar imediatamente após o clique nos CTAs do rodapé: Chat
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - OAB',
 'eventAction': 'Rodapé', 
 'eventLabel': 'CTA: {{nome-do-cta}}' //Trazer o nome do botão. Ex: Chat
});
```
&nbsp;
># Redação
&nbsp;
>### Redação - Cabeçalho 

Disparar imediatamente após o clique nos botões do menu (Como funciona, Professores, Planos e Login)
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Redação',
 'eventAction': 'Cabeçalho',
 'eventLabel': 'Botão: {{nome-do-botao}}'         //Trazer o nome do botão. Ex: Como funciona, Professores, Planos e Login
});
```
&nbsp;
>### Redação - Botão - CTA Interesse 

Disparar imediatamente após o clique nos botões de interesse (Quero enviar minha redação agora, Assistir ao vídeo demonstrativo )
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Redação',
 'eventAction': 'Botão CTA - Interesse',
 'eventLabel': 'Botão: {{nome-do-botao}}'         //Trazer o nome do botão. Ex: Entrar, Faça o teste agora, Saiba mais)

});
```
&nbsp;
>### Redação - Botão - CTA Ação

Disparar imediatamente após o clique nos botões de ação (Eu quero)
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Redação',
 'eventAction': 'Botão CTA - Ação',
 'eventLabel': 'Botão: {{nome-do-botao}} - Produto: {{nome-do-produto}}'         //Trazer o nome do botão e produto. Ex: Eu quero e 1 ano prime
});
```
&nbsp;
>### Redação - Rodapé CTA

Disparar imediatamente após o clique nos CTAs do rodapé: Chat
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Redação',
 'eventAction': 'Rodapé', 
 'eventLabel': 'CTA: {{nome-do-cta}}' //Trazer o nome do botão. Ex: Chat
});
```
&nbsp;
># Pós
&nbsp;
>### Pós - Cabeçalho

Disparar imediatamente após o clique nas opções do menu (Nossos Cursos, Professores,...)
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Pós',
 'eventAction': 'Cabeçalho',
 'eventLabel': 'Botão: {{nome-do-botão}}'   //Trazer botão do cabeçalho clicada pelo usuário, caso seja “nossos cursos” Trazer submenu clicado.  
});
```
&nbsp;
>### Pós - Botão - CTA Interesse 

Disparar imediatamente após o clique nos botões de interesse (Escolha seu curso, Play Vídeo, Conheça os professores, Saiba mais, Veja os cursos, Curso do Carrossel, Dúvidas chame aqui, Envie-nos uma mensagem, E-mail, Chat online, Envie uma mensagem, Baixe o guia do curso)
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Pós',
 'eventAction': 'Botão CTA - Interesse',
 'eventLabel': 'Botão: {{nome-do-botao}}'         //Trazer o nome do botão. Ex: Escolha seu curso, Play Vídeo, Conheça os professores, Saiba mais, Veja os cursos, Curso do Carrossel, Dúvidas chame aqui, Envie-nos uma mensagem, E-mail, Chat online, Envie uma mensagem, Baixe o guia do curso
});
```
&nbsp;
>### Pós - Botão - CTA Ação

Disparar imediatamente após o clique nos botões de ação (Matricule-se agora, Finalizar compra, Escolher esse )
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Pós',
 'eventAction': 'Botão CTA - Ação',
 'eventLabel': 'Botão: {{nome-do-botao}} - Curso: {{nome-do-curso}}'    //Trazer o nome do botão. Ex: Matricule-se agora, Finalizar compra, Escolher esse
});
```
&nbsp;
>### Pós - Rodapé Links

Disparar imediatamente após o clique nos links do rodapé: Cursos de Pós intensiva, Como funciona, redes sociais etc.
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Pós',
 'eventAction': 'Rodapé', 
 'eventLabel': 'Link: {{nome-do-link}}' //Trazer o nome do link. Ex: Cursos de Pós intensiva, Como funciona, redes sociais etc.
});
```
&nbsp;
>### Pós - Rodapé CTA

Disparar imediatamente após o clique nos CTAs do rodapé: Chat, Chat online, Envie um mensagem (whatsapp)
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Pós',
 'eventAction': 'Rodapé', 
 'eventLabel': 'CTA: {{nome-do-cta}}' //Trazer o nome do botão. Ex: Chat, Chat online, Envie um mensagem (whatsapp)
});
```
&nbsp;

># Blog
&nbsp;
>### Blog - Cabeçalho

Disparar imediatamente após o clique nas opções do menu (Início, Últimas notícias,...)
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Blog',
 'eventAction': 'Cabeçalho',
 'eventLabel': 'Botão: {{nome-do-botão}}'  //Trazer botão do cabeçalho clicada pelo usuário
});
```
&nbsp;
>### Blog - Campo de Pesquisa

Disparar imediatamente após o usuário pesquisar algo
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Blog',
 'eventAction': 'Cabeçalho',
 'eventLabel': 'Termo pesquisado: {{termo-pesquisado}}' //trazer o termo pesquisado
});
```
&nbsp;
>### Blog - Cabeçalho - Cursos

Disparar imediatamente após o clique nas opções submenu no botão cursos (Assinatura Ilimitada 6.0, Exame da ordem)
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Blog',
 'eventAction': 'Cabeçalho',
 'eventLabel': 'Botão: {{nome-do-botão}} - Cursos: {{nome-do-curso}}'  //Trazer botão do cabeçalho clicada pelo usuário, caso seja “Cursos” Trazer submenu clicado.  
});
```
&nbsp;
>### Blog - Cabeçalho - Filtros

Disparar imediatamente após o clique nas opções de filtro selecionado (Centro-oeste, AC...)
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Blog',
 'eventAction': 'Cabeçalho',
 'eventLabel': 'Filtro: {{nome-do-botão}}'  //Trazer botão do filtro selecionado: Centro-oeste, AC...
});
```
&nbsp;
>### Blog - Botão - CTA Interesse 

Disparar imediatamente após o clique nos botões de interesses: Eventos gratuitos, Assinatura Ilimitada, Em destaque, Veja mais) ou nos conteúdos (Clicou para ver edital)
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Blog',
 'eventAction': 'Botão CTA - Interesse',
 'eventLabel': 'Botão: {{nome-do-botao}}'         //Trazer o nome do botão. Ex: Eventos gratuitos, Assinatura Ilimitada, Em destaque, Veja mais) ou nos conteúdos (Clicou para ver edital)

});
```
&nbsp;
>### Blog - Botão - CTA Interesse - Player

Disparar imediatamente após o clique nos botões de interação com player de conteúdo. Ex: play, avançar, troceder, velocidade 1x, velcidade 2x.
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Blog',
 'eventAction': 'Botão CTA - Interesse',
 'eventLabel': 'Player: {{nome-do-botao}}'         //Trazer o nome do botão. Ex: Ex: play, avançar, troceder, velocidade 1x, velcidade 2x.
});
```
&nbsp;
>### Blog - Botão - CTA Ação 

Disparar imediatamente após o clique no botão de CTA. Ex: publicar comentário
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Blog',
 'eventAction': 'Botão CTA - Ação',
 'eventLabel': 'Botão: {{nome-do-botao}}'         //Trazer o nome do botão: Acompanhar (concursos); Publicar comentãrio
});
```
&nbsp;

>### Blog - Rodapé Links

Disparar imediatamente após o clique nos links do rodapé: Quem somos, Central de Ajusta, Atendimento Online, Redes sociais etc.
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Blog',
 'eventAction': 'Rodapé', 
 'eventLabel': 'Link: {{nome-do-link}}' //Trazer o nome do link. Ex: Quem somos, Central de Ajusta, Atendimento Online, Redes sociais etc.
});
```
&nbsp;
>### Blog - Rodapé CTA

Disparar imediatamente após o clique nos CTAs do rodapé: Atendimento de vendas, Foi aprovado?
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Blog',
 'eventAction': 'Rodapé', 
 'eventLabel': 'CTA: {{nome-do-cta}}' //Trazer o nome do botão. Ex: Atendimento de vendas, Foi aprovado?
});
```
&nbsp;
># Coaching
&nbsp;

>### Coaching - Cabeçalho 

Disparar imediatamente após o clique nos botões do menu (Programa, Plano e Equipe)
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Coaching',
 'eventAction': 'Cabeçalho',
 'eventLabel': 'Botão: {{nome-do-botao}}'         //Trazer o nome do botão. Ex: Programa, Plano e Equipe
});
```
&nbsp;
>### Coaching -  CTA Interesse

Disparar imediatamente após o clique nos botões de ação de interesse (Garantir minha vaga, Quero ser..., Estudar melhor, Quero falar com o GranXperts, Quero saber mais sobre os planos)
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Coaching',
 'eventAction': 'Botão CTA - Interesse',
 'eventLabel': 'Botão: {{nome-do-botao}}'         //Garantir minha vaga, Quero ser..., Quero saber mais sobre os planos
});
```
&nbsp;
>### Coaching -  CTA Ação

Disparar imediatamente após o clique nos botões de ação de lead (planos): 3 meses, 6 meses e 12 meses - modais.
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Coaching',
 'eventAction': 'Botão CTA - Ação',
 'eventLabel': 'Botão: Plano {{nome-do-botao}}'      //Botão: Plano 3 meses
});
```
&nbsp;
>### Coaching - Rodapé Links

Disparar imediatamente após o clique nos links do rodapé: Quem somos, Atendimento, Redes sociais etc.
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Coaching',
 'eventAction': 'Rodapé', 
 'eventLabel': 'Link: {{nome-do-link}}' //Trazer o nome do link. Ex: Quem somos, Atendimento, Redes sociais etc.
});
```
&nbsp;
>### Coaching - Rodapé CTA

Disparar imediatamente após o clique nos CTAs do rodapé: Saiba mais, chat
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Coaching',
 'eventAction': 'Rodapé', 
 'eventLabel': 'CTA: {{nome-do-cta}}' //Trazer o nome do botão. Ex: Saiba mais, chat
});
```
&nbsp;
># Questões
&nbsp;
>### Questões - Cabeçalho 

Disparar imediatamente após o clique nos botões do menu (Provas, Questões, Concursos, Planos, Blog e Ajuda) ou após logado (inicio, programa de estudos, assuntos frequentes, disciplinas)
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Questões',
 'eventAction': 'Cabeçalho',
 'eventLabel': 'Botão: {{nome-do-botao}}'         //Trazer o nome do botão. Ex:(Provas, Questões, Concursos, Planos, Blog e Ajuda) ou após logado (inicio, programa de estudos, assuntos frequentes, disciplinas)
});
```
&nbsp;
>### Questões - CTA Interesse - Provas

Disparar imediatamente após o clique nos botões de ação de interesses  na página de provas: Filtrar Provas, Anexos, Remover, Limpar Filtro 
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Questões',
 'eventAction': 'Botão CTA - Interesse',
 'eventLabel': 'Provas - Botão: {{nome-do-botao}}'         //Filtrar Provas, Anexos, Remover, Limpar Filtro
});
```
&nbsp;
>### Questões - CTA Interesse - Questões

Disparar imediatamente após o clique nos botões de ação de interesses  na página de questões: Filtrar questões, Responder, Limpar Filtro, Salvar filtro, Gerar simulado, Finalizar simulado, Novo simulado
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Questões',
 'eventAction': 'Botão CTA - Interesse',
 'eventLabel': 'Questões - Botão: {{nome-do-botao}}'         //Filtrar questões, Responder, Limpar Filtro, Salvar filtro, Gerar simulado, Finalizar simulado, Novo simulado
});
```
&nbsp;
>### Questões - CTA Interesse - Disciplinas

Disparar imediatamente após o clique nos botões de ação de interesses na página de discplinas: Estude agora, Discplina escolhida
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Questões',
 'eventAction': 'Botão CTA - Interesse',
 'eventLabel': 'Discplinas - Botão: {{nome-do-botao}}'         //Estude agora, Discplina escolhida
});
```
&nbsp;
>### Questões - CTA Interesse - Concursos

Disparar imediatamente após o clique nos botões de ação de interesses na página de concursos: Ver todos, Nome do concurso,Filtrar concursos, Navegar nas questões dessa prova, Estudar
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Questões',
 'eventAction': 'Botão CTA - Interesse',
 'eventLabel': 'Concursos - Botão: {{nome-do-botao}}'         //Ver todos,ou Nome do concurso, Filtrar concursos, 
});
```
&nbsp;
>### Questões - CTA Interesse - Assuntos Frequentes

Disparar imediatamente após o clique nos botões de ação de interesses na página de assuntos frequentes: Pesquisar
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Questões',
 'eventAction': 'Botão CTA - Interesse',
 'eventLabel': 'Assuntos Frequentes - Botão: {{nome-do-botao}}'         //pesquisar
});
```
&nbsp;
>### Questões - CTA Ação

Disparar imediatamente após o clique nos botões de ação de lead (Cadastre-se Gratis, Entrar, Comece Gratis, Comece agora, Começar teste grátis) ou Assinatura (Assinar plano pro mensal, assinar plano pro anual etc), Assinatura ilimitada 6.0, ver mais ou Programa de estudos Saiba mais
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Questões',
 'eventAction': 'Botão CTA - Ação',
 'eventLabel': 'Botão: {{nome-do-botao}}   //Cadastre-se Gratis, Entrar, Comece Gratis, Comece agora, Começar teste grátis) ou Assinatura (Assinar plano pro mensal, assinar plano pro anual etc), Assinatura ilimitada 6.0, ver mais ou Programa de estudos Saiba mais
});
```
&nbsp;
>### Questões - Rodapé Links

Disparar imediatamente após o clique nos links do rodapé: Como funciona, questões para concursos, redes sociais etc.
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Questões',
 'eventAction': 'Rodapé', 
 'eventLabel': 'Link: {{nome-do-link}}' //Trazer o nome do link. Ex: Como funciona, questões para concursos, redes sociais etc.
});
```
&nbsp;
>### Questões - Rodapé CTA

Disparar imediatamente após o clique nos CTAs do rodapé: Chat
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Questões',
 'eventAction': 'Rodapé', 
 'eventLabel': 'CTA: {{nome-do-cta}}' //Trazer o nome do botão. Ex: Chat
});
```
&nbsp;
># Área do Aluno
&nbsp;
>### Área do Aluno - Cabeçalho - Termo de Pesquisa 

Disparar imediatamente após a pesquisa do cabeçalho.
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Área do Aluno',
 'eventAction': 'Cabeçalho', 
 'eventLabel': 'Termo de Pesquisa: {{nome-do-cta}}' //Trazer o termo pesquisado. Ex: Polícia Civil 
});
```
&nbsp;

>### Área do Aluno - Cabeçalho - Menu Perfil

Disparar imediatamente após o clique nas opções do menu do perfil do aluno. Minha conta, perfil de estudo, formas de pagamento,...
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Área do Aluno',
 'eventAction': 'Cabeçalho', 
 'eventLabel': 'Botão: {{opção-menu-clicada}}' //Trazer a opção clicada. Ex: Minha conta, perfil de estudo, formas de pagamento,... 
});
```
&nbsp;
>### Área do Aluno - Menu Conteúdo CTA Interesse 

Disparar imediatamente após o clique em botões dentro do menu lateral à esquerda como 'Acessar todos os cursos', 'Lista de Cursos', 'Meus Cursos', 'adicionar um sonho',...
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Área do Aluno',
 'eventAction': 'Menu Conteúdo CTA Interesse', 
 'eventLabel': 'Botão: {{nome-do-botão}} - Ambiente: {{nome-do-ambiente}}' //Trazer a opção clicada. Ex:  'Botão: Acessar todos os cursos - Ambiente: Início', 'Lishta de Cursos', 'Botão: Meus Cursos - Ambiente: Meus Certificados', 'Botão: adicionar um sonho' - Ambiente: Mural dos Sonhos,...
});
```
&nbsp;
>### Área do Aluno - Menu Conteúdo CTA Ação

Disparar imediatamente após o clique nos botões 'Quero testar agora', "Quero Assinar agora', Download do APP, 'Quero ser Assinante','Upgrade para Assinatura'.
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Área do Aluno',
 'eventAction': 'Menu Conteúdo CTA Ação', 
 'eventLabel': 'Botão: {{nome-do-botao}}' //Trazer a opção clicada. Ex:  'Quero testar agora', "Quero Assinar agora', Download do APP, 'Quero ser Assinante'.
});
```
&nbsp;

>### Área do Aluno - Rodapé - CTA

Disparar imediatamente após o clique nos botões flutuantes do rodapé: Chat e pesquisa demográfica.
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'gaEvent',
 'eventCategory': 'Conteúdo - Área do Aluno',
 'eventAction': 'Rodapé - CTA', 
 'eventLabel': 'CTA: {{nome-do-cta}}' //Trazer a opção clicada. Ex:  Chat, Pesquisa demográfica.
});
```
&nbsp;
># Enhanced Ecommerce
&nbsp;
Aqui estão listadas as estruturas de dados para coleta do sistema de ecommerce. Inconsistências nas nomenclaturas das chaves ou estrutura geral dos objetos resultará em falha na coleta, pois seguimos padrões esperados pelo Google Analytics.

Caso tenham dúvidas, vocês podem usar os links abaixo como referência: https://developers.google.com/tag-manager/enhanced-ecommerce para a documentação e aqui um exemplo aplicado https://enhancedecommerce.appspot.com/

&nbsp;
>## Objeto de Produto

&nbsp;

O objeto de produto acompanha diversos disparos. Nessa seção explicamos melhor o objeto, mas ele consta como referência, e será listado novamente nos disparos onde estiver presente.


>### Objeto de Produto (todos os fluxos: OAB, Cursos para concursos, Redação, Pós, Assinatura ilimitada, Questões, Coaching, Residência e CFC):

```
{
        'id': '53648',
        'name': 'TCE PI - Tribunal de Contas do Estado do Piauí - Auditor de Controle Externo',
        'list': 'Carrossel - Home Page',
        'brand': 'GCO',
        'category': 'Cursos para concursos',
        'variant': 'semestral',
        'position': 8,
        'price': '799.90',
        'quantity': '1',
        'coupon': 'ANIVERSARIO',
        'id': '34567', //id transaction
        'revenue': '1998,67',
        'tax': '10.5',
        'shiping': '20.6',
        'step': '3',
        'option': 'boleto',
        'rendalimitada': 'sim', //customDimension3
        'genero': 'sim', //customDimension4
        'parcelas': '10x', //customDimension5
        'vagas': '301', //customDimension6
        'salarios': 'de R$4.731,91 a R$16.670,59', //customDimension7
        'regiao': 'RN', //customDimension8
        'taxainscricao': 'R$120,00 a R$150,00', //customDimension9
        'periodoinscricao': '02/12/2020 a 21/12/2020', //customDimension10
        'datadaprova': '11/07/2021 18/07/2021', //customDimension11
        'bancaexaminadora': 'FGV (Fundação Getúlio Vargas)', //customDimension12
        'instituicao': 'PC RN - Polícia Civil do Estado do Rio Grande do Norte', //customDimension13
        'escolaridade': 'Superior', //customDimension14
        'areas': 'Policiais', //customDimension15
        'taf': 'não', //customDimension16
        'redacaodiscursiva': 'sim', //customDimension17
        'provadetitulos': 'não', //customDimension18
        'matrizcurricular': '360h', //customDimension19
        'numerousuarios': '4' //customDimension20
        'formadepagamento': 'cartao' //customDimension21
}
```

Quando as informações não estiverem disponíveis na página, deixar as variáveis vazias (undefined).

`id` Id do produto selecionado. `string`  

`name` Nome do produto selecionado. `string`  

`list` Lista na qual o produto está contido no momento da interação. `string`  

`brand` Por hora podemos deixar fixo GCO. `string`  

`category` Nome da categoria que pertence o produto. Ex: OAB, Cursos para concursos, Redação, Pós, Assinatura ilimitada, Questões, Coaching. `string`  

`variant` Período de escolha do curso. Ex: Semestral, Anual, 6 a 18 meses etc. `string`  

`position` Posição numérica na qual o produto se encontra dentro do local onde é exibido. O primeiro produto deveser o número 1, o segundo o 2 e assim sucessivamente. Utilize a ordem na qual os elementossão chamados no html. `inter`

`price` Preço total do protudo em `string` com separador ponto(.).

`quantity` Quantidade de produtos em uma mesma transação. `inter`

`coupon` O cupom da transação resgatado com a transação. `string`  

`id (transaction)` Id da transação. `string` 

`revenue` Receita da transação. `number`

`tax` Se houve imposto. `number`

`shiping` Custo de envio do produto (em nosso caso não temos). `number`

`step` Um número que representa uma etapa no processo de checkout. Opcional em ações `checkout`. `inter`

`option` Campo adicional para checkoutações checkout_option que podem descrever informações de opções na página de checkout, como o método de pagamento selecionado.

`rendalimitada` - personalizada - A opção renda limitada está selecionada? `string` 

`genero` - personalizada - A opção genero feminino está selecionada? `string` 

`parcelas` - personalizada - Quantidade de parcelas da compra efetuada (se cartão) `string` 

`vagas` - personalizada - Quantas vagas o concurso possui? `string` 

`salarios` - personalizada - Salario do concurso. `string` 

`regiao` - personalizada - Região do concurso, estado ou nacional? `string`

`taxainscricao` - personalizada - Taxa de inscrição do concurso. `string` 

`periodoinscricao` - personalizada - Periodo de inscrição do concurso. `string` 

`datadaprova` - personalizada - Data de realização da prova. `string` 

`bancaexaminadora` - personalizada - Nome da banca examinadora. `string` 

`instituicao` - personalizada - Nome da instituição. `string` 

`escolaridade` - personalizada - Nível de escolaridade. `string` 

`areas` - personalizada - Áreas. `string` 

`taf` - personalizada - Sim ou não. `string` 

`redacaodiscursiva` - personalizada - Sim ou não. `string` 

`provadetitulos` - personalizada - Sim ou não. `string` 

`matrizcurricular` - personalizada - Total de horas do curso. `string`

`numerousuarios` - personalizada - Número de usuários para utilizar o produto. `string`

`formadepagamento` - personalizada - Identificar se o pagamento é via boleto, cartão, pix etc. `string`

&nbsp;
>## Impressões de produto

&nbsp;

<em>
Esses dados devem ser populados na variável de dataLayer antes da chamada do Google Tag Manager.
</em>

Documentação sobre Impressões de Produto no [link - impressions](https://developers.google.com/tag-manager/enhanced-ecommerce?hl=pt_br#product-impressions)

A chave `impressions` deve conter array com os dados de todos os produtos exibidos na tela.

Deve disparar no carregamento de qualquer tela que exiba produtos clicáveis, seguindo a seguinte estrutura:

<em>
Aplicável a todos fluxos de compra - Assinatura Ilimitada, Cursos p/ Concursos, CFC, OAB, Residência, Redação, Questões, Pós Graduação, GranXperts.
</em>

&nbsp;

>### Impressões 
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({ ecommerce: null }); // Limpa o objeto eccom anterior
dataLayer.push({
 'event': 'productImpressions_UA',
 'ecommerce': {
     'impressions': [
     {
        'name': 'Individual Social',
        'id': '53648', // Name or ID is required
        'price': '1198.80',
        'brand': 'GCO',
        'category': 'Assinatura Ilimitada',
        'variant': 'Assinatura 1 ano',
        'list': 'Página de produto - Assinatura Ilimitada',
        'position': 1
      },
     {
        'name': 'TCE PI - Tribunal de Contas do Estado do Piauí - Auditor de Controle Externo',
        'id': '53567',        
        'price': '3598.80',
        'brand': 'GCO',
        'category': 'Cursos para Concursos',
        'variant': '',
        'list': 'Página de produto',
        'position': 2
      }]
  }
});
```

Ponto a considerar, nas páginas de concursos, temos as opções de pacotes, cursos por matéria e todos os cursos. O ideal é que o impression carregue no carregamento de cada "aba". Na assinatura ilimitada, mesmo racional.

&nbsp;
>## Clique em produtos
&nbsp;

<em>
Esse objeto de dados deve ser enviado no momento que um click for realizado em um produto listado.
</em>

&nbsp;

Após esse push, o Google Tag Manager irá receber e gerar um payload para os servidores do Google Analytics. Utilizaremos no Google Tag Manager a funcionalidade de beacon dos navegadores para evitar perda de dados em caso de redirecionamento do usuário antes do envio dos dados para o Google. 

De qualquer forma, solicitamos que seja incluído um delay de meio segundo ou, para evitar perda de dados, seja utilizada a função de callback do dataLayer conforme explicado no [link - product clicks](https://developers.google.com/tag-manager/enhanced-ecommerce#product-clicks)

A chave list dentro do campo ``actionField`` deve conter o mesmo valor que estava relacionado ao produto no campo de mesmo nome do disparo de impressão.

<em>
Aplicável a todos fluxos de compra - Assinatura Ilimitada, Cursos p/ Concursos, CFC, OAB, Residência, Redação, Questões, Pós Graduação, GranXperts.
</em>

&nbsp;

>### Product Click

```
window.dataLayer = window.dataLayer || [];
dataLayer.push({ ecommerce: null });  // Clear the previous ecommerce object.
dataLayer.push({
    'event': 'productClick_UA',
    'ecommerce': {
      'click': {
        'actionField': {'list': 'Página de Projeto'}, // Optional list property.
        'products': [{
            'name': 'ASSINATURA INDIVIDUAL SOCIAL',    
            'id': '133',                // Prod ID
            'price': '1198.80',         // Preço do Produto
            'brand': 'GCO',
            'category': 'Assinatura Ilimitada',
            'variant': 'Assinatura 1 ano',
            'rendalimitada': 'sim', //customDimension3
            'genero': 'sim', //customDimension4
            'vagas': '301', //customDimension6
            'salarios': 'de R$4.731,91 a R$16.670,59', //customDimension7
            'regiao': 'RN', //customDimension8
            'taxainscricao': 'R$120,00 a R$150,00', //customDimension9
            'periodoinscricao': '02/12/2020 a 21/12/2020', //customDimension10
            'datadaprova': '11/07/2021 18/07/2021', //customDimension11
            'bancaexaminadora': 'FGV (Fundação Getúlio Vargas)', //customDimension12
            'instituicao': 'PC RN - Polícia Civil do Estado do Rio Grande do Norte', //customDimension13
            'escolaridade': 'Superior', //customDimension14
            'areas': 'Policiais', //customDimension15
            'taf': 'não', //customDimension16
            'redacaodiscursiva': 'sim', //customDimension17
            'provadetitulos': 'não', //customDimension18
            'matrizcurricular': '360h', //customDimension19
            'numerousuarios': '4' //customDimension20
         }]
       }
     },
  });
```

>## Detalhes do produto
&nbsp;

<em>
Esse disparo deve ocorrer no carregamento inicial da página de produto, ou seja, a página dedicada ao produto específico.
</em>

&nbsp;

Documentação do google no [link - details](https://developers.google.com/tag-manager/enhanced-ecommerce?hl=pt_br#details)

<em>
Aplicável a todos fluxos de compra - Assinatura Ilimitada, Cursos p/ Concursos, CFC, OAB, Residência, Redação, Questões, Pós Graduação, GranXperts.
</em>

&nbsp;

>### Detail
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({ ecommerce: null });  // Clear the previous ecommerce object.
dataLayer.push({
 'event': 'productDetails_UA', 
 'ecommerce': {
    'detail': {
      'actionField': {'list': 'Página de Projeto'},    // "detail" actions have an optional list property.
      'products': [{
            'name': 'ASSINATURA INDIVIDUAL SOCIAL',    
            'id': '133',               // Prod ID
            'price': '1198.80',        // Preço do Produto
            'brand': 'GCO',
            'category': 'Assinatura Ilimitada',
            'variant': 'Assinatura 1 ano',
            'rendalimitada': 'sim', //customDimension3
            'genero': 'sim', //customDimension4
            'vagas': '301', //customDimension6
            'salarios': 'de R$4.731,91 a R$16.670,59', //customDimension7
            'regiao': 'RN', //customDimension8
            'taxainscricao': 'R$120,00 a R$150,00', //customDimension9
            'periodoinscricao': '02/12/2020 a 21/12/2020', //customDimension10
            'datadaprova': '11/07/2021 18/07/2021', //customDimension11
            'bancaexaminadora': 'FGV (Fundação Getúlio Vargas)', //customDimension12
            'instituicao': 'PC RN - Polícia Civil do Estado do Rio Grande do Norte', //customDimension13
            'escolaridade': 'Superior', //customDimension14
            'areas': 'Policiais', //customDimension15
            'taf': 'não', //customDimension16
            'redacaodiscursiva': 'sim', //customDimension17
            'provadetitulos': 'não', //customDimension18
            'matrizcurricular': '360h', //customDimension19
            'numerousuarios': '4' //customDimension20            
       }]
     }
   }
});
```

No caso de assinatura ilimitada, detail quando o pop up estiver carregado, ou seja, no clique no produto.
Diferente do impression, que coleta os dados ao clicar nas abas, aqui queremos coletar os detalhes das informações independen de selecionar a aba "sobre o concurso" ou não.

&nbsp;

>## Adicionar ou remover do Carrinho:
&nbsp;

<em>
Esse disparo deve ocorrer quando o usuário adiciona ou remove produtos no carrinho.
</em>

&nbsp;

Documentação do google no [link - addToCart](https://developers.google.com/tag-manager/enhanced-ecommerce#add)
Documentação do google no [link - removeToCart](https://developers.google.com/tag-manager/enhanced-ecommerce#remove)

<em>
Aplicável a todos fluxos de compra - Assinatura Ilimitada, Cursos p/ Concursos, CFC, OAB, Residência, Redação, Questões, Pós Graduação, GranXperts.
</em>

&nbsp;

>### Adicionar ao Carrinho:
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({ ecommerce: null });  // Limpa o objeto eccom anterior
dataLayer.push({
  'event': 'addToCart_UA', 
  'ecommerce': {
    'currencyCode': 'BRL',
    'add': {             // 'add' actionFieldObject measures.
      'products': [{     //  adding a product to a shopping cart.
        'name': 'ASSINATURA INDIVIDUAL SOCIAL',    
        'id': '133',                // Prod ID
        'price': '1198.80',         // Preço do Produto
        'brand': 'GCO',
        'category': 'Assinatura Ilimitada',
        'variant': 'Assinatura 1 ano',
        'quantity': 1,
       }]
    }
  }
});
```

>### Remover do Carrinho:
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({ ecommerce: null });  // Limpa o objeto eccom anterior
dataLayer.push({
  'event': 'addToCart_UA', 
  'ecommerce': {
    'currencyCode': 'BRL',
    'add': {             // 'add' actionFieldObject measures.
      'products': [{     //  adding a product to a shopping cart.
       'name': 'ASSINATURA INDIVIDUAL SOCIAL',    
        'id': '133',                // Prod ID
        'price': '1198.80',         // Preço do Produto
        'brand': 'GCO',
        'category': 'Assinatura Ilimitada',
        'variant': 'Assinatura 1 ano',
        'quantity': 1
       }]
    }
  }
});
```
&nbsp;
>## Promotion (View e Click):
&nbsp;

>### Promotion (View):
Esse disparo deve ocorrer quando carregarem os banners promocionais, principalmente na home.

Documentação do Google no [link - promotion - impression](https://developers.google.com/tag-manager/enhanced-ecommerce?hl=pt_br#promo-impressions)

<em>
Aplicável a todos fluxos de compra - Assinatura Ilimitada, Cursos p/ Concursos, CFC, OAB, Residência, Redação, Questões, Pós Graduação, GranXperts.
</em>

&nbsp;

```
window.dataLayer = window.dataLayer || [];
dataLayer.push({ ecommerce: null });  // Limpa o objeto eccom anterior
dataLayer.push({
  'event': 'promoView_UA',
  'ecommerce': {
    'promoView': {
      'promotions': [                     // Array of promoFieldObjects.
       {
         'id': 'JUNE_PROMO13',   // ID do banner ( Cada banner precisa ter um código único)
         'name': 'June Sale',
         'creative': 'banner1',
         'position': 'slot1'
       },
       {
         'id': 'FREE_SHIP13',
         'name': 'Free Shipping Promo',
         'creative': 'skyscraper1',
         'position': 'slot2'
       }]
    }
  }
});
 ```

&nbsp;
>### Promotion (Click):
Esse disparo deve ocorrer quando o usuário clicar em um dos banners promocionais.

Documentação do Google no [link - promotion - click](https://developers.google.com/tag-manager/enhanced-ecommerce?hl=pt_br#promo-clicks)
<em>
Aplicável a todos fluxos de compra - Assinatura Ilimitada, Cursos p/ Concursos, CFC, OAB, Residência, Redação, Questões, Pós Graduação, GranXperts.
</em>



```
window.dataLayer = window.dataLayer || [];
dataLayer.push({ ecommerce: null });  // Limpa o objeto eccom anterior
dataLayer.push({
  'event': 'promoClick_UA',
  'ecommerce': {
    'promoClick': {
      'promotions': [                     // Array of promoFieldObjects.
       {
         'id': 'JUNE_PROMO13',   // ID do banner ( Cada banner precisa ter um código único)
         'name': 'June Sale',
         'creative': 'banner1',
         'position': 'slot1'
       }]
    }
  }
});
 ```
&nbsp;
>## Checkout
&nbsp;

Esse disparo deve ocorrer em diversos momentos do fluxo de checkout, variando apenas a chave step conforme tabela abaixo:

| ``'step'``  | Momento do disparo (curso para concurso) |
| ----------- | ----------- |
| 1           | Iniciou Carrinho |
| 2           | Identificação    |
| 3           | Pagamento        |
| 4           | Confirmação      |


Documentação do Google no [link - checkout](https://developers.google.com/tag-manager/enhanced-ecommerce?hl=pt_br#checkout)
<em>
Aplicável a todos fluxos de compra - Assinatura Ilimitada, Cursos p/ Concursos, CFC, OAB, Residência, Redação, Questões, Pós Graduação, GranXperts.
</em>

&nbsp;
>### Checkout:
```
window.dataLayer = window.dataLayer || [];
dataLayer.push({ ecommerce: null });  // Limpa o objeto eccom anterior
dataLayer.push({
  'event': 'checkout_UA',
  'ecommerce': {
      'checkout': {
        'actionField': {'step': 3, 'option': 'Boleto'}, // Ou "Cartão"
        'products': [{
          'name': 'ASSINATURA INDIVIDUAL SOCIAL',    
          'id': '133',              // Prod ID
          'price': '1198.80',       // Preço do Produto
          'brand': 'GCO',
          'category': 'Assinatura Ilimitada',
          'variant': 'Assinatura 1 ano',
          'quantity': '1'
       }]
    }
  }
});
```

Temos quatro fluxos diferentes de checkout: Concursos (Cursos, OAB, Redação e Pós), Assinatura ilimitada, Coaching e Questões. Cada um possui steps diferentes, porém o ideal é ter todos os steps nos quatro fluxos, fazendo a correspondencia correta entre eles (Ex : iniciou o carrinho é o 1 no concursos, no Assinatura ilimitada ele não existe, portanto a identificação no Assinatura deve iniciar no step 2.)

&nbsp;

>## Sucesso de Compra:
&nbsp;

Deve ser disparada após o sucesso da compra.

Documentação do Google no [link - purchase](https://developers.google.com/tag-manager/enhanced-ecommerce?hl=pt_br#purchases)
<em>
Aplicável a todos fluxos de compra - Assinatura Ilimitada, Cursos p/ Concursos, CFC, OAB, Residência, Redação, Questões, Pós Graduação, GranXperts.
</em>

&nbsp;

```
window.dataLayer = window.dataLayer || [];
dataLayer.push({ ecommerce: null });  // Limpa o objeto ecomm anterior
dataLayer.push({
 'event': 'purchase_UA', 
 'ecommerce': {
    'purchase': {
      'actionField': {
        'id': '192839089',    // ID da TRANSAÇÃO (Order ID)
        'revenue': '1078.92',  // Valor total da transação
        'tax':'',
        'shipping': '',
        'coupon': '',          // Caso haja algum cupom na COMPRA
        'parcelas': '10x', //customDimension5
        'formadepagamento': 'cartao' //customDimension21
      },
      'products': [{          // Lista de objetos de Produto
        'name': 'ASSINATURA INDIVIDUAL SOCIAL',    
        'id': '133',          // Prod ID
        'price': '1198.80',   // Preço do Produto
        'brand': 'GCO',
        'category': 'Assinatura Ilimitada',
        'variant': 'Assinatura 1 ano',
        'quantity': 1,
        'coupon': '',          // Campo opcional caso haja algum desconto no PRODUTO
        'rendalimitada': 'sim', //customDimension3
        'genero': 'sim', //customDimension4
        'vagas': '301', //customDimension6
        'salarios': 'de R$4.731,91 a R$16.670,59', //customDimension7
        'regiao': 'RN', //customDimension8
        'taxainscricao': 'R$120,00 a R$150,00', //customDimension9
        'periodoinscricao': '02/12/2020 a 21/12/2020', //customDimension10
        'datadaprova': '11/07/2021 18/07/2021', //customDimension11
        'bancaexaminadora': 'FGV (Fundação Getúlio Vargas)', //customDimension12
        'instituicao': 'PC RN - Polícia Civil do Estado do Rio Grande do Norte', //customDimension13
        'escolaridade': 'Superior', //customDimension14
        'areas': 'Policiais', //customDimension15
        'taf': 'não', //customDimension16
        'redacaodiscursiva': 'sim', //customDimension17
        'provadetitulos': 'não', //customDimension18
        'matrizcurricular': '360h', //customDimension19
        'numerousuarios': '4' //customDimension20
       },
       {
        'name': 'nomeProduto seguinte',
        'id': 'idProduto seguinte',
        'price': 'precoProduto seguinte', 
        'brand': 'GCO',
        'category': 'categProduto seguinte',
        'variant': 'variantProduto seguinte',
        'quantity': 1,
        'coupon': '',          // Campo opcional caso haja algum desconto no PRODUTO
        'rendalimitada': 'sim', //customDimension3
        'genero': 'sim', //customDimension4
        'vagas': '301', //customDimension6
        'salarios': 'de R$4.731,91 a R$16.670,59', //customDimension7
        'regiao': 'RN', //customDimension8
        'taxainscricao': 'R$120,00 a R$150,00', //customDimension9
        'periodoinscricao': '02/12/2020 a 21/12/2020', //customDimension10
        'datadaprova': '11/07/2021 18/07/2021', //customDimension11
        'bancaexaminadora': 'FGV (Fundação Getúlio Vargas)', //customDimension12
        'instituicao': 'PC RN - Polícia Civil do Estado do Rio Grande do Norte', //customDimension13
        'escolaridade': 'Superior', //customDimension14
        'areas': 'Policiais', //customDimension15
        'taf': 'não', //customDimension16
        'redacaodiscursiva': 'sim', //customDimension17
        'provadetitulos': 'não', //customDimension18
        'matrizcurricular': '360h', //customDimension19
        'numerousuarios': '4' //customDimension20
       }]
    }
  }
});
```




