# conteudo/ — piadas e áudios que os apps baixam

O app Android traz só o básico: 135 piadas com as vozes do Tio Mau e da Dona Fê (35 gravadas originais + 100 do acervo)
e as falas dos personagens. Todo o resto vem desta pasta, publicada pelo GitHub Pages.
O app só conta piada que tem a voz do personagem escolhido: nunca usa a voz do celular nas piadas.

| Arquivo | O que é |
|---|---|
| `indice.json` | Lista dos lotes e dos pacotes de áudio, com tamanho e SHA-256 |
| `piadas2/lote_NNNN.tsv` | Uma piada por linha: `id TAB pergunta TAB resposta` (o id é o nome dos áudios) |
| `audio/acervo/m/…zip` e `audio/acervo/f/…zip` | Vozes do acervo (Tio Mau / Dona Fê), 50 piadas por pacote, com os envelopes da boca |
| `piadas/lote_NNNN.txt` | Formato antigo (versão 5.3.0) |
| `piadas/extras.txt` | Piadas avulsas |
| `audio/android/pNN.zip` | Áudios das piadas gravadas, de 20 em 20 (OGG) |

## Como o app usa
- Ao abrir e durante o uso (no máximo a cada 6 horas) lê `indice.json`.
- Baixa só o lote novo ou alterado (SHA diferente), confere o SHA e passa cada piada pelo filtro de conteúdo.
- Lote que sair do índice é apagado do aparelho.
- Piadas repetidas (mesma pergunta, ignorando acentos e pontuação) são descartadas.
- Piada gravada só toca quando o áudio dela já está no aparelho; os pacotes são baixados aos poucos, um por vez.

## Como publicar um lote novo
1. Gerar o lote no acervo (`gerar_lote.py`).
2. Gravar as vozes: `python3 /home/claude/tts/gerar_acervo.py` (retoma de onde parou; ~9 piadas por minuto).
3. Rodar `python3 publicar_conteudo.py` (pasta `ferramentas` do acervo): recria lotes, pacotes e `indice.json`.
   Um pacote de voz só entra quando todas as 50 piadas dele já têm voz.
4. Subir a pasta `conteudo/` no repositório do site (arquivos iguais não mudam).
Os apps pegam o lote novo sozinhos, sem atualização na loja.

Para retirar uma piada de todos os aparelhos: apagar a linha do lote, rodar o passo 3 e subir de novo.
