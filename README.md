# Compre Fácil

Sistema de navegação inteligente integrado a carrinhos de supermercado, com localização interna de produtos, desenvolvido com foco em acessibilidade e autonomia.

**Instituição:** UNICID – Universidade Cidade de São Paulo
**Disciplina:** Gestão Ágil
**Grupo:** 09
**Atividade:** Troca de Projetos
**Local e ano:** São Paulo – SP, 2026

---

## Sumário

1. [Visão geral](#1-visão-geral)
2. [Requisitos funcionais](#2-requisitos-funcionais)
3. [Requisitos não funcionais](#3-requisitos-não-funcionais)
4. [Fluxos de uso](#4-fluxos-de-uso)
5. [Arquitetura interna](#5-arquitetura-interna)
6. [Cronograma de etapas do projeto](#6-cronograma-de-etapas-do-projeto)
7. [Limitações e expectativas do protótipo](#7-limitações-e-expectativas-do-protótipo)
8. [Identidade visual](#8-identidade-visual)
9. [Melhorias futuras](#9-melhorias-futuras)
10. [Referências](#10-referências)
11. [Equipe](#11-equipe)

---

## 1. Visão geral

O projeto Compre Fácil consiste no desenvolvimento de um sistema de navegação inteligente integrado a carrinhos de supermercado, utilizando localização interna para auxiliar os usuários durante suas compras. Por meio de uma interface no próprio carrinho, é possível pesquisar produtos e receber orientações até sua localização dentro do estabelecimento.

A solução é desenvolvida com foco em acessibilidade e autonomia, oferecendo comandos e orientações por voz, interface intuitiva e linguagem simplificada para pessoas com deficiência. Também são consideradas rotas de menor deslocamento e mais adequadas para pessoas com mobilidade reduzida, proporcionando uma experiência de compra mais acessível e eficiente.

### Tecnologias utilizadas

| Camada | Tecnologia |
|--------|------------|
| Captura de imagens | Webcam ou câmera IP |
| Processamento de vídeo | OpenCV (Python) |
| Anotação de imagens | Roboflow |
| Reconhecimento de produtos | YOLO (Python) |
| API de integração | FastAPI (Python) |
| Banco de dados | PostgreSQL |
| Interface do carrinho | HTML, CSS e JavaScript |

---

## 2. Requisitos funcionais

| Código | Descrição |
|--------|-----------|
| RF01 | O sistema deverá permitir que o usuário pesquise produtos disponíveis no supermercado. |
| RF02 | O sistema deverá informar a localização do produto pesquisado e apresentar uma rota até o seu local. |
| RF03 | O sistema deverá consultar o banco de dados do supermercado para verificar a disponibilidade dos produtos em estoque. |
| RF04 | O sistema deverá fornecer instruções de navegação por meio de comandos e orientações de voz. |
| RF05 | O sistema deverá disponibilizar uma interface com elementos visuais e linguagem simplificados, visando facilitar sua utilização por pessoas com diferentes necessidades de acessibilidade. |
| RF06 | O sistema deverá recalcular ou atualizar a rota quando necessário, considerando alterações na localização do usuário ou indisponibilidade de determinado produto. |
| RF07 | O sistema deverá exibir um aviso quando os produtos pesquisados não estiverem disponíveis. |
| RF08 | O sistema deverá permitir novas consultas de rotas para produtos após uma consulta já ter sido iniciada. |
| RF09 | Em caso de indisponibilidade de produtos, o sistema deverá oferecer recomendações de produtos semelhantes ao usuário. |

---

## 3. Requisitos não funcionais

| Código | Descrição |
|--------|-----------|
| RNF01 | O sistema deverá possuir interface simples, intuitiva e de fácil utilização. |
| RNF02 | O sistema deverá atender às necessidades de acessibilidade, oferecendo recursos de interação por voz e linguagem simplificada. |
| RNF03 | O sistema deverá garantir a confidencialidade, integridade e disponibilidade das informações processadas. |
| RNF04 | O sistema deverá permitir integração com os sistemas e banco de dados utilizados pelo supermercado. |
| RNF05 | O sistema deverá fornecer informações de localização e disponibilidade de produtos de forma consistente, reduzindo a possibilidade de orientações incorretas. |

---

<img width="1343" height="636" alt="Captura de tela 2026-11-13 200942" src="https://github.com/user-attachments/assets/44c5b860-da18-4ce9-b533-298d1ebc98d6" />


## 4. Fluxos de uso

### 4.1 Fluxo geral

1. O sistema exibe a tela inicial.
2. O usuário escolhe uma das ações disponíveis:
   - Pesquisar produto (fluxo A);
   - Lista de Compras (fluxo B);
   - Ofertas do Dia (fluxo C);
   - Chamar atendente (fluxo D);
   - Botões de configuração (fluxo E).
3. Ao concluir o subfluxo, o sistema pergunta se o usuário deseja continuar navegando.
   - Se sim, retorna à tela inicial.
   - Se não, encerra a utilização.

### 4.2 Fluxo A – Busca de produtos

1. O usuário toca no campo de pesquisa e digita o termo do produto.
2. O sistema exibe sugestões de busca.
3. O usuário toca em "Encontrar" ou "Buscar".
4. O sistema exibe os resultados da busca.
5. O usuário escolhe uma ação sobre o produto:
   - **Adicionar:** o produto é adicionado ao carrinho;
   - **Abrir detalhes:** o sistema exibe os detalhes do produto, a partir dos quais o usuário pode adicioná-lo ou rastreá-lo;
   - **Rastrear:** inicia o fluxo de rota.

**Subfluxo de rota (R)**

1. O sistema exibe a rota até o produto.
2. O usuário pode cancelar a rota (a rota é encerrada) ou seguir as instruções da rota.
3. O sistema retorna ao fluxo geral.

### 4.3 Fluxo B – Lista de compras (gerar ou importar)

**Criar lista**

1. O usuário busca o produto por nome, categoria ou sugestão.
2. O usuário toca em "+" no produto.
3. O sistema atualiza o carrinho (itens, quantidade e total).
4. O usuário pode adicionar mais produtos, repetindo o processo.
5. Opcionalmente, o usuário pode alterar a quantidade ou remover itens.
6. O usuário visualiza o carrinho e o sistema retorna ao fluxo geral.

**Importar lista**

1. O usuário escolhe o método de importação: leitura de QR Code ou digitação de código.
2. O sistema importa a lista do aplicativo e retorna ao fluxo geral.

### 4.4 Fluxo C – Aba de ofertas

O sistema exibe as ofertas do dia. O usuário pode filtrar ou navegar pelas ofertas, adicionar o produto ao carrinho ou rastreá-lo (subfluxo de rota R).

### 4.5 Fluxo D – Solicitação de auxílio humano

O sistema informa que o atendente está a caminho. O usuário pode tocar em "Voltar" ou aguardar o atendente.

### 4.6 Fluxo E – Configurações de acessibilidade

| Botão | Tipo de controle |
|-------|------------------|
| Volume | Deslizante |
| Contraste | 3 modos (Padrão, Alto Contraste e Modo Escuro) |
| Brilho | Deslizante |
| Texto | Níveis e *slider* |

---

## 5. Arquitetura interna

O funcionamento do Compre Fácil é composto por três pequenos sistemas que operam em conjunto: as câmeras de reconhecimento de produtos, a confirmação da localização oficial do produto desejado e o envio das informações e da rota ao software do carrinho.

### 5.1 Visão geral dos componentes

| Etapa | Componente | Função no sistema | Responsável / Tecnologia |
|:-----:|------------|-------------------|--------------------------|
| 1 | Câmera | Captura contínua da imagem da prateleira | Hardware (webcam ou câmera IP) |
| 2 | OpenCV | Captura o vídeo e separa em imagens (frames) | Python |
| 3 | Roboflow | Anotação de metadados (etiquetas) e *bounding boxes* nas imagens | Roboflow |
| 4 | YOLO | Leitura do vídeo e divisão em frames individuais | Python (IA) |
| 5 | Módulo de zonas | Converte a posição na imagem em corredor, prateleira e zona | Python |
| 6 | Confirmação | A mudança só vale se a nova posição ficar estável | Python (lógica) |
| 7 | API (FastAPI) | Recepção dos dados da IA e gravação no banco | Integração (Python) |
| 8 | Banco de dados | Armazenamento relacional de produtos, corredores, prateleiras e zonas | PostgreSQL (SQL) |
| 9 | Sistema do carrinho | Leitura da localização atualizada | HTML, CSS e JavaScript |

### 5.2 Captura de imagens e cuidados com a câmera

- **Monitoramento contínuo:** a câmera aponta fixamente para 2 ou 3 prateleiras.
- **Atenção operacional:** a câmera deve permanecer imóvel e bem iluminada; qualquer deslocamento desalinha as zonas virtuais.

### 5.3 Reconhecimento com o YOLO (*You Only Look Once*)

- **Saída de informações por frame:** nome do produto (por exemplo, arroz), caixa ao redor do produto com a posição na imagem e a confiança, ou seja, o grau de certeza do modelo (por exemplo, 92%). Detecções com baixa confiança são ignoradas.
- **Preparação do modelo:** 5 a 10 produtos são separados e fotografados diversas vezes, variando posição e iluminação. No Roboflow, anota-se a identificação desses produtos, desenhando a caixa de detecção ao redor de cada um e inserindo nome e informações nas etiquetas de metadados. O material é aplicado ao YOLO, testando-se se ele reconhece os produtos ao vivo.

### 5.4 Mapeamento de zonas

A prateleira é dividida em zonas virtuais (A, B e C). A IA não precisa medir distâncias em centímetros. O processo ocorre da seguinte forma:

1. O YOLO desenha a caixa em volta do produto.
2. O módulo de zonas calcula o centro da caixa. Se o centro estiver na área da Zona C, o produto está na Zona C.
3. Cada zona da imagem já foi vinculada previamente a um endereço fixo (corredor, prateleira e zona), definido uma única vez na preparação do YOLO.

### 5.5 Validação das posições

O sistema não atualiza o banco a cada imagem, pois clientes frequentemente deixam produtos fora de suas devidas áreas, o que causaria instabilidade a cada atualização. A regra adotada é:

- O banco guarda a última zona confirmada de cada produto.
- Se o YOLO detectar o produto em uma zona diferente durante vários frames seguidos (por exemplo, de 3 a 5 segundos), a mudança é confirmada.
- Somente então o sistema envia a atualização para a API.
- Caso o produto desapareça da imagem, nenhuma alteração é realizada.

### 5.6 Integração entre a IA e o sistema do carrinho

As equipes responsáveis pelo carrinho e pela API trabalham de forma independente. A integração é feita pela API (FastAPI), que grava no PostgreSQL: as câmeras apenas escrevem a localização e o sistema do carrinho somente lê as atualizações finais.

**Exemplo de atualização enviada pela IA quando um produto passa da Zona A para a Zona C:**

```http
PUT /produtos/1/localizacao
Content-Type: application/json

{"corredor": 1, "prateleira": 2, "zona": "C"}
```

**Estado da tabela no banco de dados após a mudança:**

| ID | Produto | Corredor | Prateleira | Zona |
|:--:|---------|:--------:|:----------:|:----:|
| 1 | Arroz Tio João | 1 | 2 | C |
| 2 | Feijão Kicaldo | 1 | 2 | A |
| 3 | Macarrão | 1 | 3 | B |

**Regras estritas de construção do sistema:**

- Uso estrito do mesmo ID para cada classe de produto (por exemplo, arroz = 1) nos dois sistemas;
- Formato padronizado para cada corredor, prateleira e zona;
- Definição do endereço e da porta em que a API será executada, e se o banco de dados será compartilhado;
- Designação de um responsável da equipe pelo cadastro inicial dos produtos no banco, antes da demonstração.

---

## 6. Cronograma de etapas do projeto

| Fase | Etapa | Descrição prática |
|:----:|-------|-------------------|
| 1 | Escopo inicial | Escolher 5 a 10 produtos e estruturar as zonas A, B e C na prateleira. |
| 2 | Posicionamento | Instalar e fixar a câmera de frente para a área de teste. |
| 3 | Coleta de dados | Tirar fotos dos produtos e realizar a anotação das imagens (Roboflow). |
| 4 | Treinamento | Treinar o modelo YOLO com as imagens etiquetadas e validar o reconhecimento ao vivo. |
| 5 | Mapeamento | Vincular as áreas da imagem aos endereços físicos. |
| 6 | Lógica de confirmação | Programar a regra de estabilidade de frames. |
| 7 | API e persistência | Desenvolver e testar a rota FastAPI integrada ao PostgreSQL. |
| 8 | Teste integrado | Simular a movimentação de produtos com a equipe do carrinho. |

---

## 7. Limitações e expectativas do protótipo

Por se tratar de um protótipo inicial, o escopo é reduzido:

- O monitoramento não cobre um supermercado completo, que demandaria dezenas de câmeras e produtos;
- São utilizadas zonas em vez de medidas em centímetros;
- Não são tratados casos de oclusão, iluminação baixa ou produtos idênticos.

**Validação dos resultados:** move-se um produto entre as zonas da câmera, verificando a estabilidade da IA ao atualizar o banco de dados e refletir a nova localização diretamente no carrinho.

---

## 8. Identidade visual

### 8.1 Tipografia

| Elemento | Fonte e tamanho |
|----------|-----------------|
| Títulos | Segoe UI Bold, tamanho 31 |
| Contraste | Segoe UI Bold, tamanho 12 |
| Textos | Segoe UI, tamanho 10.5 |

A formatação textual é aplicada em todo o software e nos três modos de visualização oferecidos: Padrão (tons claros), Alto Contraste e Modo Escuro. As cores principais são azul e verde, em diferentes tons, escolhidos por sua associação a serenidade, racionalidade e confiança, bem como pela harmonização com tons de branco e preto.

Para facilitar a coexistência do Compre Fácil dentro dos aplicativos de mercado, o software se adequa à paleta de cores dos supermercados. Dessa forma, mantém-se o foco do cliente no sistema principal do mercado e evita-se que o Compre Fácil seja percebido como outro mercado, em vez de um auxiliar.

### 8.2 Paleta de cores

**Modo Padrão**

| Cor | Código hexadecimal |
|-----|--------------------|
| Azul principal | `#0a5fe9` |
| Azul claro (fundo) | `#e5f4ff` |
| Verde-água | `#24d8b9` |
| Azul-marinho | `#0b2060` |
| Verde claro | `#e2fff1` |
| Amarelo claro | `#fffbd7` |
| Azul céu | `#94cdff` |

**Modo Alto Contraste**

| Cor | Código hexadecimal |
|-----|--------------------|
| Azul | `#385cfc` |
| Branco | `#ffffff` |
| Preto | `#000000` |
| Azul | `#345de6` |
| Azul-marinho escuro | `#0e1a47` |
| Amarelo | `#fbf92d` |
| Verde | `#44ef62` |

**Modo Escuro**

| Cor | Código hexadecimal |
|-----|--------------------|
| Branco | `#FFFFFF` |
| Verde-água | `#0fb5a0` |
| Azul | `#0a5fe9` |
| Azul-acinzentado escuro | `#1d2b44` |
| Marrom escuro | `#3c3629` |
| Azul profundo | `#1c3569` |
| Verde escuro | `#1a4c46` |

---

## 9. Melhorias futuras

- **Rotas personalizadas:** usuários com mobilidade reduzida receberão rotas que priorizem corredores mais vazios, facilitando a locomoção e diminuindo esforços, com apoio do sistema de reconhecimento do YOLO.
- **Variedade de contrastes e filtros de cor:** mais opções de contraste para usuários com baixa visão e filtros de correção para diferentes tipos de daltonismo (por exemplo, escala de cinza e cores invertidas).
- **Contador de estoque:** sistema integrado às câmeras que monitora as prateleiras e emite alerta automático ao identificar redução nas quantidades disponíveis.

---

## 10. Referências

- ARCANJO, Jonys. **Detecção de marcadores ArUco em streams de vídeo em tempo real com OpenCV.** Medium, 2023. Disponível em: <https://jonysarcanjo.medium.com/detec%C3%A7%C3%A3o-de-marcadores-aruco-em-streams-de-v%C3%ADdeo-em-tempo-real-com-opencv-9a3d99c667d7>
- ALVES, Gabriel. **Detecção de Objetos com YOLO – Uma abordagem moderna.** IA Expert Academy, 2020. Disponível em: <https://iaexpert.academy/2020/10/13/deteccao-de-objetos-com-yolo-uma-abordagem-moderna/>
- **FastAPI (Open Source API):** <https://fastapi.tiangolo.com/pt/>
- **Documentação PostgreSQL (GitLab):** <https://halleyoliv.gitlab.io/pgdocptbr/>
- **Meio e Mensagem – Psicologia das cores:** <https://www.meioemensagem.com.br/marketing/psicologia-das-cores>

---

## 11. Equipe

Grupo 09 – Gestão Ágil – UNICID

| Nome | RGM |
|------|-----|
| Alice de Lima | 47612614 |
| Gabriela Porfirio | 48017698 |
| Henrico Saltanian | 476981721 |
| Henrique Moura | 47610972 |
| Laura Sophia da Silva | 48128406 |
| Lucas Praxedes | 47832550 |
| Nicole Xavier | 48329002 |
| Paulo Ricardo Freitas | 47917687 |
| Tarcisio Santos | 47913061 |
| Thiago Barbante | 47856564 |
