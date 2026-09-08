# Collimator VCurve — Release history

Manual: [Collimator-VCurve-Manual.pdf](Collimator-VCurve-Manual.pdf)

## v5.8.0 — 2026-09-07

**A foto agora avisa que saiu.** Ate aqui a foto BOA era gravada em silencio
- so a falha falava - entao o tecnico nao sabia se tinha apertado direito e
apertava de novo. Agora a tela pisca 2 quadros na cor do canal e o nome do
arquivo aparece por 2,5 s. A foto gravada sai limpa: o flash entra depois.

**O aviso de versao nova ganhou reserva.** Quando o GitHub nao responde, o
app pergunta a versao ao `pl-api.2olhares.com`. Foi esse o buraco do bug do
certificado da v5.7.4: os aparelhos ficaram travados sem saber que existia
versao nova. A reserva devolve SO o numero - o endereco do download continua
cravado dentro do app, entao nada de fora pode apontar o app para outro
arquivo.

**O app passa a contar as instalacoes.** Ao abrir, manda tres coisas e nada
mais: um id sorteado que fica no arquivo de configuracao, a versao, e o nome
do sistema. Nunca manda nada sobre suas lentes, suas medidas, seus arquivos
ou suas pastas, e nunca usa o IP como identificador. Serve para o suporte
saber quantas bancadas rodam qual versao - em setembro de 2026 um bug de
certificado deixou tecnicos parados e ninguem percebeu ate um deles escrever.
O "?" do app diz isso na tela.

*Somado no servidor em 08/set, sem mexer no app:* a lista tambem registra **de
que PAIS veio a conexao** - so o pais. O IP e lido p/ descobrir isso e
descartado ali mesmo: nao e guardado, nao e registrado, e nao identifica
ninguem (o id continua sorteado, nao derivado do endereco).

## v5.7.4 — 2026-09-04

Conserta o update no Windows. O app dizia "sem internet" enquanto o navegador
abria o GitHub na mesma maquina - aconteceu com o Lucas e com o Martin. O log
do tablet deu a causa: CERTIFICATE_VERIFY_FAILED, "unable to get local issuer
certificate". Nao era internet nem firewall: o Windows so baixa certificados
raiz quando alguem pede, e quem pede e o navegador; o Python nao pede. Agora o
app leva a propria lista de raizes junto (certifi) - a verificacao continua
LIGADA, so deixou de depender do que a maquina ja tinha guardado. Vale p/ o
aviso de versao nova, p/ o download da atualizacao e p/ o envio de relato.
Junto: a mensagem parou de chamar todo problema de rede de "sem internet".
Agora separa sem internet, algo bloqueando o app, falha de certificado e
servidor recusou - e mostra o motivo tecnico na propria tela do "?", sem
precisar abrir o log. Medicao (PONTO/CSV/FIT) identica.

## v5.7.3 — 2026-09-04

Acertos de uso achados na bancada logo depois da v5.7.2. Depois de tocar
ENVIAR no relato, a tela ficava aberta com so um CANCELAR na frente e parecia
que nada tinha sido enviado; agora ela vira "RELATO ENVIADO", o "enviado!
obrigado" aparece grande e verde, o teclado e o ENVIAR somem (nada de mandar
duas vezes) e fica um botao OK p/ fechar quando voce quiser. Se der erro a
tela continua como era, porque e nela que mora o botao E-MAIL de reserva.
O botao do zoom maximo estava sempre escrito MAX, mesmo ja no maximo, entao
nao dava p/ saber que o proximo toque volta p/ 1x; agora ele mostra o que o
toque vai fazer: MAX quando esta em 1x, e 1x quando esta ampliado. O idioma
PADRAO de uma instalacao nova passa a ser ingles (quem ja escolheu segue com
a escolha). E no CONFIG o botao de trocar de camera dizia CHANGE, igual ao
botao da pasta; agora diz CAM. Por fim, o ROI passa a LEMBRAR onde
estava: na bancada o reticulo fica sempre no mesmo lugar, entao o
retangulo volta no lugar quando voce reabre o app. Se ele nao couber no
quadro de hoje (voce trocou de camera ou de resolucao), volta ao centro
em vez de medir fora da imagem.

Camera que cai por mau contato no cabo agora VOLTA sozinha: depois de 3
tentativas no mesmo lugar o app varre todos os indices, porque o USB
reenumera e a camera costuma reaparecer noutro. E se voce for no CONFIG
e tocar na propria camera que caiu, ela reabre de verdade - antes esse
toque nao fazia nada e a tela ficava preta ate voce fechar e abrir o
app. O seletor tambem para de mostrar a miniatura velha de uma camera
que ja morreu. Abertura: a escada de resolucao comeca pela ultima que
funcionou (em MAX cai de 8 para 4 pedidos, medido), e o log ganha uma
linha 'abertura:' com o tempo de cada etapa - se ainda demorar, o
relato agora leva o log e da p/ ver exatamente onde.
Medicao (PONTO/CSV/FIT) identica.

## v5.7.2 — 2026-09-04

Relato de bug com ANEXOS: o botao ENVIAR RELATO agora manda junto o
colimador_log.txt, a config e o diag_*.csv gravado na sessao, e voce pode
enviar sem escrever nada - so tocar ENVIAR. A tela mostra numa linha o que
vai junto. Sem internet, o e-mail de reserva leva as ultimas 30 linhas e o
caminho dos arquivos p/ anexar a mao. Update: quando falha, o app agora diz
o que houve (sem internet x GitHub recusou) e grava a causa no log; espera
10 s em vez de 5; e se a API do GitHub recusar, ele le a versao pela pagina
de releases, que nao tem limite de pedidos. Camera que cai deixou de
congelar em silencio: aparece "religando..." sobre a imagem. Botao DESFAZER
novo (tecla u): tira o ultimo ponto, entao um numero de micrometro digitado
errado nao obriga mais a LIMPAR e refazer a varredura. O portao de qualidade
do FIT ficou honesto: ele julga so os pontos que entraram na parabola, entao
uma varredura de um lado so passa a ser marcada invalida. Trocar resolucao,
trocar camera ou abrir o DRIVER com a camera caida nao derruba mais o app.
Medicao (PONTO/CSV/FIT) identica a v5.7.1.

## v5.7.1 — 2026-09-03

Uma pasta so: CSV, fotos, DIAG e o log (agora colimador_log.txt) ficam na
pasta de saida; config.json passa ao app-data do SO (lido uma vez do lugar
antigo); Documents real em qualquer idioma; a pasta antiga some se ficar
vazia. Camera: exposicao travada de verdade (le e reescreve exposure/gain;
CONFIG AUTO/TRAVADA — o DIAG do Martin provou AE viva), modo de 30 fps
re-assertado apos escolher MAX (era 15 fps), loop ao vivo mede so o canal
exibido (mais fps em maquinas fracas), pico sobe mesmo a 12 fps. Tela:
AUTO-LAYOUT — em telas 16:9 o painel encolhe p/ 180 px (video +7,6%); em
3:2/16:10 os botoes vao p/ a faixa embaixo e o video toma a largura toda
(+30%); zoom (- + MAX) e RESET % fora do video; CONFIG em 2 colunas com
canal, idioma, camera e exposicao (painel fica com PONTO FIT LIMPAR CONFIG
FOTO). DIAG grava posicao do ROI e fps da camera e zera o pico ao comecar.
Medicao (PONTO/CSV/FIT) identica. Dica: ajuste o diafragma, RESET %, foque.

## v5.7.0 — 2026-09-03

Relato do Martin (mohrlens) + council de 02/set: o MAX era envenenado pelo
arrasto do ROI (cada retangulo intermediario era medido; um sliver sobre a
barra do reticulo da +194% e ficava como pico ate LIMPAR) - corrigido; MAX e %
agora nascem da mesma janela de 0,35 s (mediana), entao 100% e alcancavel;
botao MAX 0 zera o pico sem apagar os pontos; drift de resolucao zera o pico;
ROI desenhado do centro para fora (toque no alvo e arraste); faixa inferior com
sparkline menor e % em digitos grandes; DIAG 120 s no "?" (ou tecla d) grava
CSV com metrica, media/desvio do ROI, gx2/gy2 e exposicao/ganho lidos da camera
- e o instrumento para separar luz, desfoco e vibracao. Medicao (PONTO/CSV/FIT)
identica a v5.6.0. Dica: nao cace 100% - 5 pontos nos flancos + FIT.

## v5.6.0 — 2026-08-31

Auditoria de 31/ago (council + Codex + Codex adversarial + pre-mortem do
Martin): FIT nao crasha mais (posicoes repetidas, numero infinito, pasta
read-only, disco cheio); gate de qualidade (vertice fora da varredura ou sem 2 pontos por
lado = invalido); CSV grava o RESULTADO do fit + versao/camera/ROI e nao se
sobrescreve; camera que some nao derruba nem congela o app (religa sozinho)
e resolucao que a camera nao entrega e revertida; camera que muda de
resolucao sozinha e detectada (badge vermelho, PONTO bloqueado); update:
download conferido, troca do .app com rollback, fechar a janela nao corrompe
mais a instalacao, e o update nao interrompe varredura com pontos na
memoria; piso de 1280 valendo p/ camera pequena (teclado/botoes sempre no
canvas); leitura %/rms/max visivel tambem no tablet; log persistente em
~/Documents/colimador/colimador.log + crash log; config.json atomico;
Documents real no Windows com OneDrive; teclas c/q pedem confirmacao como
os botoes.

## v5.5.1 — 2026-08-31

- Fixes the side panel not responding to clicks/taps in v5.5.0 when the
  capture resolution is larger than the on-screen video (e.g. the new
  1080p default on a FullHD monitor) — one boundary check was left on
  the old coordinate space. Found by Martin (mohrlens). If v5.5.0 left
  you stuck: keyboard shortcuts (space, f, ESC) still worked, and this
  update restores the panel.

## v5.5.0 — 2026-08-31

- **Camera resolution is now configurable** in SETTINGS: 720p / **1080p
  (new default)** / MAX (up to 4K). The measurement runs on the full
  chosen resolution — in our synthetic bench study, 1080p roughly
  doubles vertex precision with long lenses and on the 65 mm master.
  Changing it clears the current points (different metric scale), and
  the CSV filename now records the resolution used.
- **Display decoupled from capture**: the live view scales to your
  screen (a FullHD/4K monitor automatically shows more real pixels),
  zoom keeps showing true camera pixels, and a badge at the top right
  shows the actual resolution and frame rate.
- Switching cameras now adopts the new camera's real frame size instead
  of stretching it to the old one.

## v5.4.5 — 2026-08-31

- Fixes the "everything doubled at startup" glitch seen on some Windows
  machines (Intel graphics): the window now opens **already maximized**
  and forces a full repaint, so the compositor can no longer blend the
  old window surface over the new one — which also made buttons hard to
  hit.
- **Single-instance guard**: opening the app twice now shows "already
  running" briefly and closes the extra copy, instead of stacking two
  windows on top of each other.
- The window appears **instantly** with an "opening..." splash while
  cameras are probed — no more silent seconds inviting a second click.

## v5.4.4 — 2026-08-29

- Configurable **max zoom**: 5× (default) or 10×, in SETTINGS next to
  the zoom step. Double-tap and the direct-to-MAX step follow whatever
  ceiling you pick.

## v5.4.3 — 2026-08-29

- Zoom now defaults to smooth **5% steps** per wheel/pinch notch (a
  continuous scroll glides from 1× to 5× in about a second) instead of
  jumping straight to 5×. The 2× step and the direct-to-MAX behaviour
  remain available in SETTINGS, and double-tap still toggles 1× ↔ 5×.

## v5.4.2 — 2026-08-29

- **One-tap silent update**: the update dialog now downloads the new
  version and applies it by itself, then reopens the app — Windows via
  the new installer, macOS by swapping the app from the `.dmg`, Linux by
  replacing the binary in place. If automatic update is not possible
  (offline, `.deb` install, unusual setup) it falls back to opening the
  download page.
- **Proper installers**: Windows now ships as
  `CollimatorVCurve-setup.exe` — install, update or repair by simply
  running it (per-user, no admin needed). Internally the app is an
  unpacked folder, which avoids Windows Defender's `Wacatac.B!ml` false
  positive that hit the v5.4.0 single-file `.exe`. Linux gains a `.deb`
  package with a menu entry (the raw binary is still published). macOS
  keeps the drag-to-Applications `.dmg`.

## v5.4.1 — 2026-08-29

- Readable live readout, bench-multimeter style: the graph still runs at
  video rate, but the numbers now update ~3×/s showing the window
  average — digits hold still between updates. The big number is now
  **% of peak** (the natural readout when hunting a maximum); rms, max
  and the raw value stay as a smaller line with 3 significant digits.

## v5.4.0 — 2026-08-28

**New**

- **SETTINGS** button (replaces DRIVER, which now lives inside it on
  Windows): configurable **photos & CSV folder** (with an OPEN shortcut),
  zoom step, and gesture switches.
- **View zoom** centered on the ROI (display only — the measurement always
  uses the raw image): pinch / Ctrl+wheel, on-screen **− / +** buttons,
  `+`/`-` keys, and **double-tap** jumps straight to 5×.
- **Peak hold** on the focus graph (dashed line + max) and an **RMS**
  readout next to the raw metric.
- The micrometer pad opens with the **previous value pre-selected** —
  just type to replace it.
- **?** menu: **SEND REPORT** (in-app message box, delivered straight to
  support), **CHECK FOR UPDATE** and **MANUAL**.
- The app checks for new versions at startup and asks before opening the
  download page.

**Fixed**

- The **± uncertainty** of the FIT was inflated when micrometer readings
  were far from zero (a covariance term was dropped). The vertex itself
  was always correct; only the reported ± changes.
- A dropped camera frame during POINT no longer biases the metric low.
- Unplugging the camera no longer freezes the app.
- A stray tap on the image no longer resets the ROI.

## v5.3.2 — 2026-08-07

- Maximized window with no black bars on any screen shape; large
  sparkline strip under the video.
- CLOSE and **?** (help) buttons in the side panel.

## v5.3.0 — 2026-08-04

- **Mirror tilt** measured during the scan and reported with FIT results
  (the image centroid traces a spiral as the micrometer spindle turns).
- CSV gains the centroid columns `cx_px, cy_px`.

## v5.2.0 — 2026-07

- App renamed **Collimator VCurve**.
- Camera selector with a **live thumbnail** per input; last camera
  remembered.
- Keypad: negative sign and **mm | µm** input toggle (persisted).
- First PDF manual.

## v5.1.1 — 2026-07-17

- macOS: camera permission fixed in the `.dmg` build (the app looked like
  it would not open).

## v5.1.0 — 2026-07-16

- PT/EN language toggle; window opens maximized.
- First builds for the three platforms (Windows / macOS / Linux).
