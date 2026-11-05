# JPlayer

Player de música offline (PWA) com IA.

## Publicar no GitHub Pages
1. Crie um repositório no GitHub (ex.: `jplayer`).
2. Envie todos os arquivos desta pasta para a raiz do repositório.
3. Em **Settings → Pages**: Source = *Deploy from a branch*, Branch = `main` / `(root)` → Save.
4. Aguarde 1–2 min e abra `https://SEU-USUARIO.github.io/jplayer/` no Chrome do celular.
5. Menu ⋮ → **Instalar app** / **Adicionar à tela inicial**.

## Transformar em app Android (APK/AAB)
1. Com o site no ar, abra https://www.pwabuilder.com e cole a URL do GitHub Pages.
2. Clique em **Package for stores → Android** e baixe o pacote.
3. Instale o `.apk` no celular (ou use o `.aab` na Play Store).

## Atualizar
Ao mudar o app, aumente o número em `CACHE` no `service-worker.js` (ex.: `jplayer-v26`). O app abre sempre pelo cache (instantâneo) e baixa a versão nova em paralelo: ela aparece na abertura seguinte.

## IA do chat
- **Fila, não playlist:** o que você pede para tocar vai só para a fila. A IA **nunca cria playlist sozinha**: só cria quando você pedir (ex.: "cria uma playlist de rock"). Essa regra também é travada no código, não só na conversa.
- Nome repetido não substitui nada: a nova vira "Nome (2)".
- Pedidos que ela entende: tocar (a fila vira só o pedido), "coloca X na fila" (sem interromper), tocar uma playlist sua, adicionar em playlist existente, salvar a fila como playlist, pular, voltar, pausar, embaralhar, limpar fila, favoritar e mudar o volume.
- Ela sabe o que está tocando, a fila, suas favoritas, as mais tocadas, as recentes e as suas playlists.
- "Apaga as playlists automáticas" remove as que a versão antiga criou sozinha (nome termina com data, ex.: "Para hoje · 01/11"), sempre pedindo confirmação.
- A cada mensagem, a IA recebe o catálogo **atualizado** da biblioteca (títulos, artistas e estilos). Música nova importada já é conhecida na próxima mensagem.
- Ao adicionar músicas, a IA avisa no chat e classifica o estilo delas (com internet).
- Biblioteca muito grande: a IA vê os artistas principais + as músicas mais relevantes ao pedido.
- Sem internet (ou com a opção "só no Wi-Fi" ligada no 4G/5G), o chat usa o modo local: estilos, climas e artistas.

## Letras automáticas
- Toda música importada tem a letra procurada e salva sozinha (LRCLIB, precisa de internet). Se a música já traz letra no arquivo, ela é mantida.
- Ao abrir o app, as músicas que ainda estão sem letra entram na fila. Sem internet, a busca continua quando a conexão voltar.
- Letra não encontrada é tentada de novo depois de 7 dias; o botão "Buscar letra online" tenta na hora.
- A opção "só no Wi-Fi" também vale para a busca de letras.
- A letra aparece num cartão colorido embaixo do player (botão "Letra"). Quando existe versão sincronizada, a linha atual acompanha a música, e tocar numa linha pula para ela.

## Jplay Wrapped e Jplay Guess (Ajustes)
- Wrapped: o app registra cada reprodução (a partir de 15 s ouvidos) no próprio aparelho. As estatísticas são calculadas só com esse histórico real, por mês ou por ano, em formato de stories, e cada card pode ser compartilhado como imagem.
- Guess: o jogo usa só os arquivos da sua biblioteca, tocados no próprio aparelho. Modos: diário, Endless, Artist e Hardcore, com recorde, histórico e ranking pessoal. Os resultados também aparecem no Wrapped.

## Abertura
- Ao abrir o app, a imagem do ícone aparece quebrada e se reconstrói em cerca de 2 s. Some sozinha, não bloqueia o app e é desativada quando o aparelho está com "reduzir movimento".

## Segundo plano (sem travar)
- Ao acabar uma música, o app não avisa mais o sistema de "pausado" entre uma faixa e outra, e sem crossfade reaproveita o mesmo player de áudio. Isso evita o Android congelar o app na troca de faixa com a tela apagada.
- Se o sistema suspender o áudio avançado (equalizador/crossfade), ele é retomado sozinho.
- Música com erro de leitura é pulada (para depois de 5 erros seguidos).
- Com o app escondido: não atualiza a tela (só ao voltar), e pausam a busca de letras e a geração de miniaturas.
- Ao voltar do segundo plano o app abre pelo cache, sem esperar a internet.

## Editar e excluir músicas
- Toque nos três pontinhos de qualquer música (lista ou player) e escolha **Editar nome e artista** ou **Excluir música**.
- Editar: muda o nome da música e do artista. Se o artista tiver mais músicas, dá para ligar "Trocar em todas as músicas" e corrigir tudo de uma vez. As edições ficam salvas e não voltam ao normal.
- Excluir: pede confirmação e remove do JPlayer, das playlists, dos favoritos e da fila. O arquivo original no celular não é apagado.

## Segundo plano (atualização)
- O app agora sempre lembra a música, a fila e o ponto onde parou, mesmo se o Android fechar o app com a música pausada.
- A fila é salva ao esconder o app, e o app pede armazenamento persistente para o Android não apagar suas músicas.

## Trocar capa e velocidade
- Trocar capa: menu da música (três pontinhos) → Editar nome e artista → **Trocar capa**. A imagem da galeria é cortada em quadrado e salva. **Remover** volta à capa original.
- Velocidade: toque em **Velocidade** no menu da música para alternar 0,75x, 1x, 1,25x, 1,5x e 2x, ou escolha em Ajustes → Player. Vale para todas as músicas e o tom não muda.

## Visualizador de som
- Fica no player completo, entre o título e a barra de progresso, em largura total. O grave pulsa no centro e os agudos nas pontas, seguindo o áudio real (equalizador incluso).
- Ajustes → Player: "Visualizador de som" liga/desliga e "Reagir ao grave e agudos" escolhe o áudio real. Se o app voltar a fechar em segundo plano, desligue essa opção.

## Barra de onda (estilo Lark Player)
- No player completo, a barra de progresso vira a forma da música: a parte já tocada fica na cor de destaque. Toque ou arraste para pular.
- A forma é calculada do áudio real, uma vez por música, quando você a abre no player (músicas com mais de 8 min ou 45 MB mostram uma forma aproximada). Fica salva depois.
- Com "Reagir ao grave" ligado, as barras perto do ponto atual pulsam com o grave.
- Ajustes → Player: "Barra de onda", "Reagir ao grave" e "Visualizador acima do título" (o visualizador grande agora vem desligado).

## Instalar / baixar o app
- Ajustes → Geral tem um cartão **Instalar o JPlayer**: com o botão quando o Chrome libera a instalação, ou com o passo a passo quando não libera. Na Home também aparece um botão quando a instalação está disponível.
- Se o Chrome não instalar (comum em Xiaomi/Poco): permita Configurações → Apps → Chrome → **Instalar apps desconhecidos**, abra o app 2 vezes com internet e tente de novo.
- Para um **APK** de verdade, use o passo "Transformar em app Android" acima (PWABuilder).

## Ondas em movimento
- A linha de progresso voltou ao normal (arraste nela para pular). As ondas ficam em cima da linha, crescendo de baixo para cima, e se mexem com a música: com "Reagir ao grave" ligado usam o som real; desligado, fazem um movimento suave sem usar o áudio do app.

## Ondas animadas (v25)
- As ondas ficam em cima da linha de progresso e dançam com a música: cada batida (grave) cria uma ondulação que sai do ponto atual para os dois lados. Sem "Reagir ao grave", elas dançam com um ritmo simulado.
- O desenho agora reinicia sozinho se parar, e abre junto com o player completo.

## Ondas minimalistas (v26)
- Ondas mais baixas (38 px), com 44 barras grossas e arredondadas, e movimento suave: sobem rápido na batida e descem devagar.
