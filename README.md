# Projeto Embrio

WebGIS da cadeia da reprodução humana assistida e do congelamento de oócitos, construído por
integração de bases administrativas independentes — CNES/DataSUS, RAIS/ESTAB e SisEmbrio/Anvisa.

- **São Paulo capital** (mapa principal): https://aikiesan.github.io/Projeto_Embrio/
- **Brasil** (visão nacional): https://aikiesan.github.io/Projeto_Embrio/brasil/

## Método

Nenhuma base sozinha responde à pergunta. A RAIS registra atividade econômica e vínculos formais,
não procedimentos; o CNES registra serviço cadastrado, não produção; o SisEmbrio registra produção
reportada, mas só de centros regulados. O mapa cruza os três e mantém explícito o que cada ponto
tem de evidência.

### Âncoras

Centros que reportaram ao SisEmbrio/Anvisa produção e congelamento de embriões em São Paulo capital
(2025). É o único elo com **registro nacional de armazenamento**. A conciliação com o CNES foi feita
por razão social e CEP, com escore de similaridade: 25 confirmados, 3 dentro de complexos
institucionais (HC-FMUSP, SPDM, SES-SP — unidade exata não identificável pelo nome), 3 conciliados
só por CEP e 1 sem correspondente no CNES. Cada ponto informa como foi conciliado.

### Elos da cadeia (ligados por padrão)

| Camada | Critério |
|---|---|
| Âncoras — CRHA/BCTG regulados | SisEmbrio/Anvisa |
| Bancos e criopreservação | banco de sêmen, gametas, embriologia ou criopreservação no nome CNES |
| Centros de reprodução assistida | nome CNES declara RHA, sem reporte próprio ao SisEmbrio |
| Laboratórios e apoio diagnóstico | SADT no mesmo CEP de um elo |
| Consultórios de fertilidade | termo de fertilidade no nome, sem evidência de laboratório |
| Candidatos RAIS não identificados | CEP com CNAE 8630-5/07 ou 8640-2/14 sem correspondente no CNES |

### Camadas temáticas (desligadas por padrão)

Varredura dos 29.477 estabelecimentos CNES ativos na capital por 12 grupos de palavras-chave:
reprodução assistida, fertilidade, embriologia, criopreservação e bancos, genética, medicina fetal,
endocrinologia, andrologia/urologia, ginecologia/obstetrícia, laboratórios, maternidades e
transporte. São pistas de afinidade com a cadeia, **não** confirmação de oferta de congelamento de
óvulos.

### Camadas de contexto

Clusters, densidade ponderada pelos embriões congelados, os 96 distritos de São Paulo tingidos pelo
número de elos, e raio de 1 km em torno das âncoras.

## Dados

```
data/sp_capital.json     elos da cadeia em SP capital + contagem por distrito
data/temas_sp.json       1.529 estabelecimentos das camadas temáticas
data/distritos_sp.json   96 distritos de SP, simplificados de 7,2 MB para 77 KB
brasil/data/estabelecimentos.json   298 estabelecimentos no país
```

## Geolocalização e precisão

Coordenadas vêm do endereço declarado no CNES (`NU_LATITUDE`/`NU_LONGITUDE`) — círculos cheios.
Pontos tracejados são conciliados apenas pelo CEP e caem no centro dele. Registros cujo CEP só
devolve o centroide do município ficam **fora do mapa** e aparecem em lista à parte, com logradouro
e bairro reais: em São Paulo capital um CEP pode cobrir um trecho inteiro de avenida, e fingir
precisão seria pior do que admitir a lacuna.

## Limitações

1. Congelamento de **óvulos** exige confirmação sanitária específica (licença da vigilância local,
   escopo de BCTG). Nenhuma camada aqui confirma isso por si só.
2. O **transporte** de gametas e embriões praticamente não existe nas bases — 5 registros na capital.
   Depende de empresa regularizada na vigilância sanitária local, a levantar por pedido formal.
3. Clínica, laboratório de embriologia, BCTG e empresa empregadora podem ser CNPJs distintos. O mapa
   preserva cada registro em vez de fundi-los em uma "clínica".
4. A camada SisEmbrio cobre, nesta versão, São Paulo capital.

## Fontes

- [CNES/DataSUS](https://dadosabertos.saude.gov.br/dataset/cnes-cadastro-nacional-de-estabelecimentos-de-saude) — estabelecimentos, agosto de 2026
- RAIS/ESTAB — Ministério do Trabalho e Emprego; CNAE [8630-5/07](https://concla.ibge.gov.br/busca-online-cnae.html?view=subclasse&tipo=cnae&versao=10&subclasse=8630507) e 8640-2/14
- SisEmbrio/Anvisa — Sistema Nacional de Produção de Embriões
- [codigourbano/distritos-sp](https://github.com/codigourbano/distritos-sp) — distritos
- BrasilAPI — geocodificação de CEP

Mapas base sem chave de API: CartoDB, OpenStreetMap, Esri e OpenTopoMap.
