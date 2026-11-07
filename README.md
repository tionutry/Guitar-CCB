# DigitaHinos FingerStyle

PWA estático, sem backend obrigatório, com tema escuro/bege, catálogo de hinos, player Web Audio, braço de violão em canvas, partitura/tablatura, opções, exportação textual de tablatura, gravação de tela quando suportada, instalação PWA e suporte inicial a MusicXML compactado (`.mxl`).

## Estrutura

- `index.html`: aplicação inteira (HTML, CSS e JavaScript).
- `hinos/001.mxl` … `hinos/480.mxl`: coloque aqui os arquivos do repertório.
- `hinos/index.json`: catálogo `[{"n":1,"t":"Título"}]`.
- `hinos/cifras.json`: acordes Cantoral no formato `{"N":{"k":[[compasso,tempo,raiz,tipo]]}}`.
- `sw.js`, `manifest.json`, `icons/`: PWA e cache offline.
- `pro-config.js`, `apps-script/`: validação Pro opcional.
- `.github/workflows/build-apk.yml`, `capacitor.config.json`: base para build Android.

## Executar e publicar

1. Copie os seus `001.mxl` a `480.mxl` para `hinos/` e substitua `hinos/index.json` e `hinos/cifras.json` pelos arquivos definitivos.
2. Teste em servidor HTTP local (não abra `index.html` via `file://`): `python -m http.server 8000`.
3. Publique todo o conteúdo da pasta na raiz de um repositório GitHub.
4. Em Settings → Pages, escolha Deploy from a branch, branch `main`, pasta `/ (root)`.
5. Acesse a URL HTTPS publicada. A primeira visita instala o shell; os hinos são armazenados no cache conforme forem abertos e usados online. Para cachear antecipadamente os 480 MXL, abra cada hino uma vez ou implemente precache no SW (pode exceder quotas de armazenamento).

## MusicXML e fidelidade musical — importante

O leitor MXL do protótipo extrai o primeiro XML de partitura e lê a primeira parte/voz para produzir notas e duração aproximada. Ainda não é um renderizador MusicXML completo: não implementa corretamente todas as vozes SATB, repeats/voltas, anacruse, ligaduras, claves/transposição instrumental, compassos compostos, ritornelos, articulações ou layout profissional de partitura. O desenho de partitura é uma visualização simplificada e o PDF é exportado como texto `.txt` nesta versão, não PDF vetorial. O áudio é síntese plucked-string por ruído filtrado, não gravação de violão real. A harmonização atual é demonstrativa; os algoritmos Simples/Melhor encaixe/Cantoral completos e a digitação otimizada de mão esquerda ainda precisam ser implementados e validados contra a coleção real.

Portanto, esta entrega é uma **base funcional/protótipo**, não atende integralmente ao critério de fidelidade musical e não deve ser anunciada como versão final até validar os 480 MXL e implementar as rotinas acima.

## Pro

Por padrão, tom/transposição fica bloqueado no modo gratuito. Para habilitar Pro, configure o Apps Script e a URL em `pro-config.js`. O Apps Script usa código de uso único vinculado ao identificador local do navegador; não é proteção antifraude forte.

## Atualização offline

Ao publicar uma versão, altere `CACHE_NAME` em `sw.js` para forçar novo cache. Navegadores exigem HTTPS para instalação PWA, exceto localhost.
