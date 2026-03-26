# ValidaNFe · Análise IBS/CBS em Massa

> Ferramenta web client-side para análise em lote de arquivos XML de NF-e, identificando conformidade com as novas tags de impostos **IBS** e **CBS** da Reforma Tributária brasileira.

---

## Visão Geral

Com a Reforma Tributária, as Notas Fiscais Eletrônicas (NF-e) passaram a exigir novas tags de impostos dentro da estrutura:

```xml
<imposto>
  <IBSCBS>
    <gIBSCBS> ... </gIBSCBS>
  </IBSCBS>
</imposto>
```

O **ValidaNFe** permite que contadores, analistas fiscais e desenvolvedores carreguem centenas de XMLs de uma vez e identifiquem imediatamente quais notas **ainda não possuem** a tag `<gIBSCBS>` — ou seja, aquelas que ainda precisam ser adequadas ao novo padrão.

---

## Funcionalidades

| Funcionalidade | Descrição |
|---|---|
| 📂 Upload em lote | Seleção múltipla de arquivos `.xml` via clique ou arrastar e soltar |
| 🔢 Contador imediato | Exibe quantos XMLs foram carregados logo após a seleção |
| ▶ Validação em lote | Percorre e analisa todos os arquivos ao clicar em "Validar XMLs" |
| 📊 Barra de progresso | Exibe "X de Y XMLs analisados" com barra visual animada no topo da tela |
| 🎯 Filtro inteligente | Tabela exibe **apenas** as notas sem a tag `<gIBSCBS>` |
| 📋 Cards de resumo | Total analisado, conformes e não conformes em destaque |
| ✅ Banner de parabéns | Exibido quando 100% dos XMLs estão em conformidade |
| ↺ Reset completo | Botão "Novo Upload" recarrega a página via `location.reload()` |

---

## Como Usar

### Pré-requisitos

Nenhuma instalação necessária. O sistema funciona **100% no navegador**, sem backend, sem servidor.

### Execução

1. Faça o download do arquivo `nfe-validador.html`
2. Abra diretamente no navegador (duplo clique no arquivo)
3. Selecione ou arraste os arquivos `.xml` para a área de upload
4. Clique em **▶ Validar XMLs**
5. Aguarde a análise — a barra de progresso indicará o andamento
6. Consulte os resultados na tabela e nos cards de resumo

> **Nota:** Somente arquivos com extensão `.xml` são aceitos. Outros formatos são ignorados automaticamente.

---

## Estrutura da Análise

O sistema verifica a presença da tag `<gIBSCBS>` em cada XML e extrai os seguintes dados de cada nota:

| Campo da Tabela | Tag XML lida |
|---|---|
| **Emitente** | `<emit><xNome>` |
| **Destinatário** | `<dest><xNome>` |
| **Chave NF-e** | `<chNFe>` |
| **Status IBS/CBS** | Presença ou ausência de `<gIBSCBS>` |

### Lógica de filtro

```
SE <gIBSCBS> presente  →  Nota CONFORME  (não aparece na tabela)
SE <gIBSCBS> ausente   →  Nota NÃO CONFORME  (exibida na tabela com badge laranja)
SE todos conformes     →  Banner verde de parabéns é exibido
```

---

## Tecnologias Utilizadas

| Tecnologia | Uso |
|---|---|
| HTML5 | Estrutura da aplicação |
| [TailwindCSS](https://tailwindcss.com) (via CDN) | Estilização e layout responsivo |
| JavaScript Vanilla | Lógica de leitura e validação dos XMLs |
| [DOMParser API](https://developer.mozilla.org/en-US/docs/Web/API/DOMParser) | Parsing nativo de XML no lado do cliente |
| [FileReader API](https://developer.mozilla.org/en-US/docs/Web/API/FileReader) | Leitura dos arquivos locais |
| [Google Fonts](https://fonts.google.com) | Tipografia: Sora + IBM Plex Mono |

---

## Estrutura do Projeto

```
/
└── nfe-validador.html   # Aplicação completa em arquivo único
└── README.md            # Este documento
```

Todo o CSS, JavaScript e HTML estão contidos em um **único arquivo `.html`** para facilitar a distribuição e o uso local sem necessidade de servidor web.

---

## Segurança e Privacidade

- ✅ Nenhum dado é enviado a servidores externos
- ✅ Todo o processamento ocorre no próprio navegador do usuário
- ✅ Os arquivos XML nunca saem da máquina local
- ✅ Não requer conexão com a internet após o carregamento inicial da página (exceto para fontes via Google Fonts e TailwindCSS via CDN)

> Para uso completamente offline, substitua os links de CDN por versões locais do TailwindCSS e das fontes.

---

## Compatibilidade

Testado e compatível com os principais navegadores modernos:

| Navegador | Suporte |
|---|---|
| Google Chrome 90+ | ✅ |
| Mozilla Firefox 88+ | ✅ |
| Microsoft Edge 90+ | ✅ |
| Safari 14+ | ✅ |

---

## Contexto: Reforma Tributária e NF-e

A Reforma Tributária brasileira (Emenda Constitucional nº 132/2023) instituiu o **IBS** (Imposto sobre Bens e Serviços) e a **CBS** (Contribuição sobre Bens e Serviços), substituindo tributos como ICMS, ISS, PIS e COFINS. A SEFAZ exige a inclusão das novas tags no layout da NF-e para refletir essa mudança. Empresas e emissores que ainda não atualizaram seus sistemas de emissão de nota fiscal aparecerão listados nesta ferramenta.

---

## Licença

Este projeto é de uso livre para fins internos e comerciais. Não há garantias expressas ou implícitas quanto à precisão da validação fiscal — sempre consulte um contador ou especialista tributário para decisões legais.

---

*Desenvolvido para ambiente local · Processamento 100% client-side · Nenhum dado enviado ao servidor*
