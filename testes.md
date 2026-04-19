# teste 1

100% original. qse perfeito. compila certo, mas qnd eu tento abrir o pdf com o view pdf latex do latex workshop ele procura na pasta build e n da certo. o pdf ta na pasta proj1. 

OK

# teste 2

mudei o settings.json pra n precisar da pasta build (excluida) e o viewer voltar a prestar.

OK

{
  // ===== BUILD =====
  "latex-workshop.latex.outDir": "%DIR%",
  "latex-workshop.latex.autoBuild.run": "onSave",

  // ===== MÁGICA VISUAL (Esconde os arquivos auxiliares) =====
  "files.exclude": {
    "**/*.aux": true,
    "**/*.bbl": true,
    "**/*.bcf": true,
    "**/*.blg": true,
    "**/*.fdb_latexmk": true,
    "**/*.fls": true,
    "**/*.log": true,
    "**/*.run.xml": true,
    "**/*.synctex.gz": true,
    "**/*.out": true,
    "**/*.lof": true,
    "**/*.lot": true,
    "**/*.toc": true
  },

  // ===== PDF VIEW =====
  "latex-workshop.view.pdf.viewer": "tab",
  "latex-workshop.view.pdf.internal.synctex.keybinding": "double-click",

  "latex-workshop.latex.tools": [
    {
      "name": "lualatex",
      "command": "lualatex",
      "args": [
        "-interaction=nonstopmode",
        "-synctex=1",
        "%DOC%"
      ]
    },
    {
      "name": "biber",
      "command": "biber",
      "args": [
        "%DOCFILE%"
      ]
    }
  ],
  "latex-workshop.latex.recipes": [
    {
      "name": "lualatex -> biber -> lualatex*2",
      "tools": [
        "lualatex",
        "biber",
        "lualatex",
        "lualatex"
      ]
    }
  ]
}

# teste 3

exclui o leia_me.txt e botei no readme.md; exclui o latexmkrc;
OK

# teste 4

movi o instructions.tex pro Textual
OK

# teste 5

movi a pasta normas pra root
OK

# teste 6

fiz mudanças e desfiz.
OK


# teste 7

live share - share read/edit - colei o link na guia anonima - entrar como anonimo - aceitei como read/write

guest: ctrl S (pra compilar)

host: compilou e atualizou o latex pdf view [OK]

# teste 8

settings.json add:
"
  "latex-workshop.viewer.pdf.internal.token": "lamec",
  "latex-workshop.view.pdf.external.host": "127.0.0.1",
  "latex-workshop.view.pdf.external.port": 65051,
  "liveshare.sharedServers": [65051],
"

processo manual:

host

- abri o vs code
- liguei o live share normal
guest
- entrei no live share
host
- TEX> abrir no navegador
- copiei o link
- adicionei o &token=lamec no final do link
guest
- colei o link do direto no simple browse

[OK]

# teste 9

.vscode/settings.json :

"
  "latex-workshop.viewer.pdf.internal.token": "lamec",
  "latex-workshop.view.pdf.external.host": "127.0.0.1",
  "latex-workshop.view.pdf.internal.port": 65051,
  "liveshare.sharedServers": [65051],
"

.vscode/tasks.json :

"
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "Lamec: Gerar Link PDF",
      "type": "process",
      "command": "powershell",
      "args": [
        "-NoProfile",
        "-Command",
        "$p = 'file:///${fileDirname}/main.pdf'.Replace('\\', '/'); $b = [Convert]::ToBase64String([System.Text.Encoding]::UTF8.GetBytes([uri]::EscapeDataString($p))); $u = 'http://localhost:65051/viewer.html?file=pdf..' + $b + '&token=lamec'; $c = '[CLIQUE AQUI PARA ABRIR O PDF NO VS CODE](command:simpleBrowser.show?[\"' + $u + '\"])'; $f = '${fileDirname}/VER_PDF.md'; $c | Out-File -FilePath $f -Encoding utf8; Write-Host 'Deu certo! Abra o arquivo VER_PDF.md' -ForegroundColor Green"
      ],
      "problemMatcher": [],
      "presentation": {
        "echo": false,
        "reveal": "always",
        "focus": true,
        "panel": "shared",
        "clear": true
      },
      "group": {
        "kind": "build",
        "isDefault": true
      }
    }
  ]
}
"

host: live share settings: allow guest task control
host: live share settings: anonymous guest approval accept
host: launcher client visualStudioCode

guest: ctrl shift B pra ver o pdf

dario testou como guest em rede diferente, deu certo com a porta 65051 shared, mas ele teve q botar o meu IP 127.0.0.1

[OK] + o latex pdf view padrão dele tbm mostrou o compilado perfeito, caso isso seja o caso geral ent n precisa do build task e do markdown

# teste 10

coloquei os arquivos VER_PDF.md e o tasks.json em uma pasta com nome zzzzzzzzzz e os renomeei pra pararem de funcionar. 

dario testou de novo com o viewer padrão da lupa do latex workhop.

mudamos a cor de fundo do pdf viewer

[OK]

# teste 11

fechamos tudo, abri de novo e vou compartilhar o live share

a intenção é testar sesmn compartilhar o terminal

settings: tirei a permissão do guest de rodar tasks

criei o server share 65051

[OK]

# teste 12

reorganizei o settings.json

"{

  // MISC SETTINGS ========================================
  //"latex-workshop.view.pdf.invert": 1, //1 for black theme | 0 for white (default) theme
  "latex-workshop.view.pdf.color.dark.pageColorsBackground": "#1e1e1e", // custom pallete
  "latex-workshop.view.pdf.color.dark.pageColorsForeground": "#ebdbb2",

  // ===== VS CODE SETTINGS ===============================
  // Prevent VS code from closing (and disconnecting live share) for updates
  "update.mode": "none",
  "extensions.autoUpdate": false,

  // ===== LIVE SHARE SETTINGS ============================
  "latex-workshop.view.pdf.viewer": "tab",
  "latex-workshop.view.pdf.internal.synctex.keybinding": "double-click",
  "liveshare.publishDiagnostics": true, // Allow the guest to write
  // Shared PDF viewer network (I would not change it)
  "latex-workshop.viewer.pdf.internal.token": "lamec",
  "latex-workshop.view.pdf.external.host": "127.0.0.1",
  "latex-workshop.view.pdf.internal.port": 65051,
  "liveshare.sharedServers": [65051],

  // ===== LATEX WORKSHOP SETTINGS ========================
  // Hide auxiliar files (except .synctex(busy) for progress tracking)
  "files.exclude": {
    "**/*.aux": true, "**/*.bbl": true, "**/*.bcf": true, "**/*.blg": true,
    "**/*.fdb_latexmk": true, "**/*.fls": true, "**/*.log": true, 
    "**/*.run.xml": true, "**/*.synctex.gz": true, "**/*.out": true,
    "**/*.lof": true, "**/*.lot": true, "**/*.toc": true
  },
  // Build settings
  "latex-workshop.latex.outDir": "%DIR%", // make possible the files tree for many people
  "latex-workshop.latex.autoBuild.run": "onSave", // allows the guest to compile with ctrl + S on Live Share
  "latex-workshop.latex.tools": [
    {
      "name": "lualatex",
      "command": "lualatex",
      "args": [
        "-interaction=nonstopmode",
        "-synctex=1",
        "%DOC%"
      ]
    },
    {
      "name": "biber",
      "command": "biber",
      "args": [
        "%DOCFILE%"
      ]
    }
  ], // compile references properly and use lualatex as main compiler
  "latex-workshop.latex.recipes": [
    {
      "name": "lualatex -> biber -> lualatex*2",
      "tools": [
        "lualatex",
        "biber",
        "lualatex",
        "lualatex"
      ]
    }
  ] // make a functional recipe that use the tools and prevent errors

}"

intenção: mostrar erros (output) e progresso de compilação do jeito mais leve possivel

o ngc de colocar o guest como read/write por padrão não funcinou 
settings.json: "liveshare.publishDiagnostics": true,

funcionou pra mostrar os "problemas", erros, avisos do latex.

desisti da barra de progresso. fica pro dario...

[OK]

# teste 13

intenção: implementar uma nuvem ou aacesso online. 

[delayed]

nova intenção: voltar a funcionar o setup, parou de compilar com ctrl S no guest, parou o viewer...

- é o ltex workshop o responsavel por fzer o pdf viewer no guest e o output
- pr funcionar, tem q o guest botar pr compilr nunca e o host onsave nsa config de user (e n na pasta .vscode) ""latex-workshop.latex.autoBuild.run": "onSave"" ""latex-workshop.latex.autoBuild.run": "never""

- add `pdfborder=0 0 0` pro hypersetup tirar as bordas de links (tema escuro corrigido) [removido]
- comentei as `Xbordercolor` do hypersetup porque nem tava usando mesmo [removido]

aparentemente funcionou pro dario depois de um temmpo sem mexer em nda

[NOT OK]

# teste 14

intenção: voltar a funcionar o setup e tentar quebrar pra ver problemas e fixes

solo de novo. 
abri o vs code, vs code insiders;
host:
share read/write
share server 65051
guest: 
join
log in with microsoft
trust workspace

demorou d+; saí e repeti o processo do guest
demorou de novo
logou rápido pelo MS edge como anonimo

compilei pelo host com ctrl S, atualizou o pdf normalmente

guest: 
join aas anonymous
trust workspace
host:
make read/write
guest:
abri o pdf viewer na lupa [ok]
editei e compilei [ok]
atualizou normal [ok]

nãao tinha output

descoobri q no output, tenho q optar por ver o output do latex workshop, ai ele fica pingando o host e da td q eu queria ver

compilei como guest de novo e vi os logs

[OK]

# teste 15

fechei a tudo

o vscode insiders (meu guest) tava bugando no login microsoft, desativei o native broker

abri o vs code, vs code insiders;
host:
share read/write
share server 65051
guest: 
join
log in with microsoft
trust workspace

ja deu join como read/write (os alunos devem logar em contas no vscode)

guest:
abri o pdf viewer na lupa [not ok, quando eu abro na web vem com port diferente da 65051]
editei e compilei [ok]
atualizou normal [not ok, aind n abriu como antes]

guest: 
sai da session
joined como anonimo
host:
permissão reaad/write
guest: o pdf abre normalmente kkkkkkkk, bizarro

eu botei em abrir pdf com browser (na aba do latex workshop), veio com porta 61134 e abriu normal, tbm abre normal tabbed dentro doo vs code na lupa

se eu for noo live share > shared server > copiar o link da 65051, ele me da localhost:54898, q n pega, mas se eu mudar pra http://127.0.0.1:54898/viewer.html?file=pdf..dnNscyUzQSUyRmFsdW5vMSUyRnByb2oxJTJGbWFpbi5wZGY tbm funciona

eu to achando estranhho q eu n consegui fzer isso como guest logado na microsoft.

de novo:

guest: 
sai da session
joined logado na microsoft
o pdf abriur normalmente kkkkkkkk, mais bizarro ainda... no teste 14 simplismente n quis

eu botei em abrir pdf com browser (na aba do latex workshop), veio com porta 59712 e abriu normal, tbm abre normal tabbed dentro doo vs code na lupa

se eu for noo live share > shared server > copiar o link da 65051, ele me da http://localhost:56666/, q n pega, mas se eu mudar pra http://127.0.0.1:56666/viewer.html?file=pdf..dnNscyUzQSUyRmFsdW5vMSUyRnByb2oxJTJGbWFpbi5wZGY tbm funciona

No Teste 14, como o processo de "Trust Workspace" e o carregamento do Insiders demoraram muito, a extensão do LaTeX Workshop tentou se conectar antes do túnel do Live Share estar 100% pronto e estável, o que resultou em perdas de comunicação (Reset connection to host )

[OK]

# teste 16

portas aleatórias

intenção: testar Race Condition, para que o aluno não precise seguir um ritual pra abrir o vs code. se der um problema, deve ter um fix. apenas. forçar o erro e corrigir.

roteiro:
*****Fase 1: Causando Amnésia no Guest (Simulando o Dia 1)
    [x] Abra o seu Guest (Insiders).
    [x] Clique no ícone de Conta (perfil) lá embaixo e faça Sign Out da Microsoft.
    [x] Aperte Ctrl + Shift + P, digite Manage Workspace Trust e remova qualquer menção ao Live Share ou ao seu Host de lá.
    [x] Feche o Guest.

*****Fase 2: O Teste do "Tropeço" (Simulando o Teste 14)
    [x] Inicie a sessão no Host e copie o link.
    [x] Abra o link no Guest.
    [x] Faça o login devagar. Leia a tela de Trust Workspace com calma e demore uns 15 segundos para clicar em "Trust".
    [deu isso, mas funcionou normalmente] O que observar: Olhe o Output do LaTeX Workshop no Guest. Você vai ver os erros de ENOENT, as portas mudando loucamente e o Reset connection to host. O túnel não estava pronto quando a extensão acordou.

Fase 3: O Teste do "Uso Diário" (Simulando o Teste 15)
    [x] Feche o Guest (mas não deslogue nem tire o Trust).
    [x] Abra o link do Live Share de novo.
    [x] O que observar: Como ele não vai pedir login nem Trust, o Guest vai "pingar" no Host muito rápido. O túnel abre em 2 segundos, a extensão do LaTeX acorda, vê que está tudo lá, e o PDF funciona liso.

[OK]

*****A "Bala de Prata" para o Dia 1 (O único comando que o aluno precisa saber)

Se no primeiro dia o aluno demorar para logar, a extensão se perder e o PDF não abrir ou a lupa não funcionar, ele não precisa sair e entrar de novo.

Ensine apenas este "botão de reset" mágico:
    [] Aperte Ctrl + Shift + P
    [] Digite Reload Window e dê Enter.

[náo precisei]

guest: 
Ctrl+S
compilou
atualizou

[OK]

# Teste 17: A Quebra Intencional (Syntax Error)

Intenção: Testar se o aluno consegue identificar erros no código sem precisar do terminal, e se o sistema sobrevive a uma falha de compilação.
Roteiro:

    Com o Host e Guest conectados, vá no Guest e escreva um comando LaTeX quebrado propositalmente (ex: \textb{teste sem o f} ou esqueça de fechar uma chave {).

    Dê Ctrl + S.

    O que observar no Guest: * O PDF não deve atualizar (vai manter a última versão boa).

        O ícone inferior esquerdo do VS Code (um "X" dentro de um círculo) deve piscar.

        Aperte Ctrl + Shift + M (Aba Problems/Problemas). O erro traduzido pelo LaTeX Workshop deve aparecer ali, apontando a linha exata.

    A Recuperação: Conserte o erro no Guest, dê Ctrl + S de novo e veja se o PDF volta a atualizar sozinho.

[OK]

# teste 18 O Escritor Cego (IntelliSense e Citações)

Intenção: Verificar se a inteligência do LaTeX Workshop (que está rodando no Host) consegue viajar pelo túnel para ajudar o aluno a digitar mais rápido no Guest. Se isso falhar, o aluno vai ter que decorar os comandos.
Roteiro:

    No Guest, vá no meio do texto e digite: \begin{

    O que observar: O VS Code mostra uma caixinha sugerindo figure, table, equation?

    Digite um comando de citação: \cite{ (ou aperte Ctrl + Space dentro das chaves).

    O que observar: Uma lista suspensa com os autores e artigos que estão no seu arquivo references.bib deve aparecer para o aluno selecionar. Se isso não aparecer, o Guest não está conseguindo ler o cache do Biber no Host.



[]

# teste 19 Concorrência (O Teste Multijogador)

Intenção: Simular dois alunos trabalhando no mesmo arquivo ou no mesmo projeto ao mesmo tempo para ver como o motor de compilação do Host reage a múltiplos Ctrl + S.
Roteiro:

    Mantenha o Host aberto.

    Abra o Insiders (Guest 1).

    Abra uma aba no navegador (Edge/Chrome) e entre pelo Live Share Web, ou use o VS Code normal se não for o Host (Guest 2).

    Coloque os dois Guests lado a lado.

    Salve os arquivos em rápida sucessão (Guest 1 dá Ctrl + S, e um segundo depois o Guest 2 dá Ctrl + S).

    O que observar: O Host vai tentar compilar duas vezes. Ele enfileira as compilações ou dá erro de "File Lock" (arquivo ocupado)? O .synctex(busy)  dá conta de mostrar que o servidor está suando a camisa?

[]

# teste 20 O Teste do "Multiverso" (Projetos Isolados Simultâneos)

Intenção: Garantir que o Host consegue compilar dois projetos completamente diferentes ao mesmo tempo, sem misturar os arquivos auxiliares e sem que o PDF de um aluno atualize na tela do outro. Como todos usam o mesmo túnel (porta 65051), a rota do PDF precisa ser blindada.
Roteiro:

    Crie aluno1/proj1/main.tex e aluno2/proj1/main.tex. Coloque textos bem diferentes neles (Ex: Título "Projeto Batman" e Título "Projeto Homem de Ferro").

    Guest 1 abre o main.tex do Aluno 1 e clica na Lupa para ver o PDF.

    Guest 2 (pode ser aba anônima no browser) abre o main.tex do Aluno 2 e clica na Lupa.

    Os dois apertam Ctrl + S exatamente ao mesmo tempo.

    O que observar:

        No Host: O Gerenciador de Tarefas deve mostrar dois processos lualatex.exe rodando paralelos.

        Nos Guests: O PDF do Batman piscou e atualizou só na tela 1? O do Homem de Ferro só na tela 2? (O LaTeX Workshop usa aquele código maluco em Base64 no link do PDF justamente para não cruzar as telas, precisamos confirmar se isso aguenta o tranco).

[]

# teste 21 O Teste "Google Docs" (Colaboração no Mesmo Projeto)

Intenção: Testar a fila de compilação do Host quando duas pessoas editam e salvam o mesmo arquivo (projx1/main.tex) freneticamente.
Roteiro:

    Guest 1 e Guest 2 abrem o mesmo projx1/main.tex.

    Guest 1 edita a introdução. Guest 2 edita a conclusão.

    Guest 1 dá Ctrl + S. Um segundo depois (antes da compilação terminar), Guest 2 dá Ctrl + S.

    O que observar:

        O LaTeX Workshop tem um sistema de "Kill". Ele vai matar a primeira compilação do Guest 1 e iniciar a do Guest 2 para não gerar arquivo corrompido? Ou vai colocar em fila?

        O PDF final mostra as edições dos dois alunos?

        Alguém recebe o erro de "File Lock" (Arquivo em uso)?

[]

# teste 22 A Queda de Energia (Teste de Resiliência)

Intenção: Alunos usam o Wi-Fi da UFPI, que pode oscilar. Precisamos saber se uma queda de internet quebra o túnel da Lupa (porta 65051) permanentemente.
Roteiro:

    Com o PDF aberto e funcionando no Guest, desligue o Wi-Fi/cabo de rede do computador do Guest por 5 segundos.

    O Live Share vai chiar que perdeu a conexão.

    Ligue a internet novamente e espere o Live Share reconectar automaticamente.

    Dê Ctrl + S.

    O que observar: O PDF atualizou? Se a Lupa ficou "surda" após a queda, teste usar a sua "Bala de Prata" (Ctrl + Shift + P -> Reload Window ) para ver se ela ressuscita a conexão do visualizador em 5 segundos sem o aluno precisar te chamar.

[]

# teste 23 Queda do Host e Retorno (O Apocalipse)

Intenção: Simular o pior cenário: o computador do laboratório (Host) travou, o Windows reiniciou sozinho ou o VS Code fechou do nada. Como os alunos sobrevivem e como o laboratório se recupera?
Roteiro:

    Host e Guest conectados, trabalhando felizes.

    No Host, feche o VS Code abruptamente (use Alt + F4 ou feche pelo Gerenciador de Tarefas para simular um crash).

    O que observar no Guest: A sessão vai cair. Aparece alguma mensagem de erro feia? O código que o aluno não salvou foi perdido?

    Reabra o VS Code no Host e inicie uma nova sessão do Live Share (um novo link será gerado).

    Mande o link novo para o Guest.

    O que observar no Guest: O aluno consegue entrar direto e continuar da onde parou? A Lupa do PDF se reconecta à porta 65051 automaticamente ou ele precisa dar um Reload Window para limpar o cache da sessão antiga?

[]

# teste 24 AFK - Inatividade (A Síndrome do Café)

Intenção: Descobrir como o túnel da porta 65051 e o próprio Live Share reagem quando o aluno abandona o PC logado por muito tempo. O Live Share tem mecanismos de economia de recursos que podem "adormecer" a sessão.
Roteiro:

    Com Host e Guest conectados e o PDF aberto, edite algo e compile (Ctrl + S) para garantir que está tudo 100%.

    Deixe o Guest completamente intocável por 30 a 45 minutos (não mova o mouse, não minimize a janela).

    Volte ao Guest, digite uma nova frase e dê Ctrl + S.

    O que observar: * O Live Share desconectou o aluno por inatividade?

        O Host compilou o código? (Olhe se a bolinha de salvamento sumiu).

        O PDF atualizou sozinho?

    O Fix: Se o PDF travou e ficou "surdo", use a Bala de Prata (Ctrl + Shift + P -> Reload Window). Meça quanto tempo leva para o aluno voltar à ativa.

[]

# teste 25 O Buraco Negro (Loop Infinito no LaTeX)

Intenção: Simular um erro grave de código (um comando recursivo, pacote conflitando, ou erro de sintaxe bizarro) que faça o LuaLaTeX entrar em um loop infinito. Precisamos saber se um aluno travado derruba o PC da UFPI para os outros.
Roteiro:

    No Guest, crie um documento e coloque o seguinte código "maldoso" no meio do texto: \def\foo{\foo}\foo (Isso cria um loop infinito clássico no TeX).

    Dê Ctrl + S.

    O que observar:

        A compilação nunca vai terminar. A bolinha vai ficar girando para sempre.

        Vá no Host (PC da UFPI) e abra o Gerenciador de Tarefas. A CPU vai estar com um núcleo em 100% pelo processo lualatex.exe.

        Enquanto o Guest 1 está travado no loop, o Guest 2 consegue salvar e compilar o projeto dele normalmente?

        O LaTeX Workshop tem um timeout padrão? Ele mata o processo sozinho após alguns minutos?
        O Fix: O Host (ou o próprio Guest) pode precisar apertar Ctrl + Shift + P -> LaTeX Workshop: Kill LaTeX compiler process para desengasgar o servidor.

[]

# teste 



[]

# teste 



[]

# teste 



[]


# TODO
[OK, so esperar o synctex sumir] mostrar o processo de compilaçção de aalgum jeito (de preferencia sem o terminal)
[NOT OK, maybe impossible] como coloca guest poor padrão read/write