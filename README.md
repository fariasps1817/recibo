# RICTEC · Emissor de Recibos

Aplicação web de página única para o **Ricardo (RICTEC)** emitir recibos de forma
rápida pelo celular. Sem banco de dados, sem servidor — roda 100% no navegador.

## O que faz

- Preenchimento em poucos toques: cliente, serviço, valor e forma de pagamento.
- Serviços pré-cadastrados (manutenção odontológica, serralheria, artesanato em
  ferro, manutenção preventiva) + campo livre.
- **Valor por extenso automático** (padrão de recibo brasileiro).
- Numeração automática e sequencial dos recibos.
- Pré-visualização do recibo (colapsável) com a logo da empresa.
- **Exportar em PDF** pela impressão nativa do navegador — folha **A4 retrato**,
  recibo ocupando a **metade superior** com linha de corte, texto nítido (vetorial).
- **Enviar por WhatsApp**: no celular, compartilha o **PDF em anexo** pela folha de
  compartilhamento nativa (Web Share API); onde não houver suporte, envia o resumo
  em texto.
- **Dados do emitente** (nome, CPF, telefone, endereço, cidade) salvos no próprio
  aparelho — preenche uma vez e não precisa repetir.

> Recibo simples, sem valor fiscal.

## Como rodar

É um site estático. Basta abrir `index.html` no navegador, ou servir a pasta:

```bash
# opcional, para testar localmente
python -m http.server 8080
# depois acesse http://localhost:8080
```

## Estrutura

| Arquivo | Descrição |
|---|---|
| `index.html` | Aplicação completa (HTML + CSS + JS, logo e manifest embutidos). |
| `jspdf.umd.min.js` | Biblioteca de geração de PDF (local, sem CDN). |
| `netlify.toml` | Configuração de publicação no Netlify. |
| `r.jpeg` | Logo da RICTEC (também usada como ícone). |
| `ri.jpeg` | Panfleto original com os dados da empresa. |

## Deploy no Netlify

1. Acesse https://app.netlify.com e faça login.
2. **Add new site → Import an existing project → GitHub** e escolha o repositório
   `fariasps1817/recibo`.
3. Build command: *(vazio)* · Publish directory: `.` (já definido no `netlify.toml`).
4. **Deploy**. A cada `git push` na branch `main` o site atualiza sozinho.

## Tecnologia

HTML, CSS e JavaScript puro. O recibo em PDF é **desenhado vetorialmente** com o
[jsPDF](https://github.com/parallax/jsPDF) (servido localmente, sem CDN): texto
nítido, coordenadas exatas em folha **A4 retrato**, sem rasterização — portanto
nunca sai truncado ou desconfigurado, em qualquer aparelho. O botão *Baixar PDF*
baixa o arquivo diretamente; o *WhatsApp* gera o mesmo PDF e o compartilha em anexo
pela folha nativa do celular (com fallback para texto onde não houver suporte).
