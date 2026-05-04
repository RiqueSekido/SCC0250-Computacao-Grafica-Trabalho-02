# SCC0250-Computacao-Grafica-Trabalho-02
# Projeto 2 - Computação Gráfica (SCC0250): "Casa no Meio do Nada"

## Integrantes
- Henrique Drago, NUSP: 14675441
- Henrique Yukio Sekido, NUSP: 14614564

## Descrição do Projeto
Este projeto consiste na construção de um cenário 3D interativo utilizando malhas Wavefront (`.obj`) texturizadas. O tema central é a **"Casa no Meio do Nada"**, um ambiente isolado e árido explorável através de uma câmera com matrizes *Model*, *View* e *Projection*.

O desenvolvimento foi feito em Python utilizando exclusivamente o pipeline moderno do OpenGL, sem recursos de iluminação.

## Construção do Cenário e Ilusão de Óptica
O cenário é dividido em dois ambientes principais com pisos distintos:
* **Interno (Casa):** Mobiliado com cama, sofá, mesa, fogão, micro-ondas, relógio, entre outros.
* **Externo (Deserto/Estrada):** Contém árvores mortas, um ponto de ônibus, um ônibus, entre outros.

### Explicação do Céu (Skybox)
Para criar a sensação de imensidão, o céu foi implementado por meio de *shaders* únicos e operações de profundidade específicas. Dessa forma, ele é sempre renderizado no fundo da cena, sendo impossível alcançá-lo. Essa técnica garante que o céu sempre pareça estar no horizonte, reforçando o isolamento da casa no meio do deserto.

### Armazenamento e Geração do Cenário (JSON)
A implementação utiliza arquivos JSON para guardar as informações e os estados dos objetos entre as sessões do programa. Para complementar a ilusão de infinitude do ambiente, a estrada e o chão foram gerados automaticamente e salvos em arquivos JSON separados, permitindo a repetição dos modelos em larga escala para compor a vasta extensão do deserto e da rodovia.

## Funcionalidades e Controles

### Navegação
* **Mouse:** Rotaciona a visão (Yaw/Pitch).
* **Scroll:** Zoom (FOV).
* **H / N:** Mover para frente/trás.
* **B / M:** Mover para os lados.
* **P:** Ativa/Desativa o modo de malha poligonal (*Wireframe*).
* **Ctrl + Shift + Alt + Super (Tecla Windows / Command no Mac) + K:** Desativa o modo restrito, permitindo a movimentação livre da câmera e o livre controle de todos os objetos do cenário.

### Transformações Especiais
As transformações geométricas obrigatórias foram aplicadas com comportamentos customizados:

1.  **Translação com Atrito (Ônibus):** As setas **Cima/Baixo** aceleram o veículo. Ao soltá-las, o ônibus para gradualmente devido a um efeito de atrito simulado no código.
2.  **Rotação por "Carga" (Spinner):** Segurar as setas **Esquerda/Direita** acumula energia. O objeto só gira quando a tecla é solta, descarregando a velocidade acumulada até parar lentamente.
3.  **Escala Animada (Relógio):** Ao apertar **A**, o relógio entra em modo "alarme", pulsando sua escala através de uma função matemática baseada no tempo.

## Como Executar
1. Instale as dependências: `pip install glfw PyOpenGL pyglm numpy pillow`.
2. Execute o arquivo `Trabalho_2.ipynb` em um ambiente Jupyter ou VSCode.
