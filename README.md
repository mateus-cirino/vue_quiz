## Sobre o quiz
Aplicação simples que a partir do carregamento de perguntas da [API](https://opentdb.com/api_config.php)  é possível salvar sua resposta, ir para a pergunta anterior ou para a próxima, além de exibir um painel com o status de cada pergunta (respondida ou não) e no final, exibe quantos pontos você fez. *(No começo eu iria exibir quais você acertou e quais errou, mostrando no caso do erro, a alternativa correta, porém acabei me concentrando em outras coisas da faculdade e do meu estágio)*.

## O que aprendi?

Fiz essa aplicação para entender um pouco do modo de trabalho do Vue, e no final eu aprendi o workflow da seguinte forma:
	Tenho um componente pai (APP) e este comunica com seus filhos (HEADER, QUESTIONBOX, NAVEGAÇÃO e RESULTADO) através de props e estes por sua vez, emitem eventos para sinalizar ao pai alguma mudança.
	Caso você esteja começando a aprender Vue, recomendo este [vídeo](https://www.youtube.com/watch?v=4deVCNJq3qc&t=3507s).

## Como testar?
*(É necessário ter o NPM)*
 1. Clonar (baixar) o repositório
 2. Abra o terminal, navegue até a pasta vue-quiz e execute `npm install`
 3. Após isso execute `npm run serve`

## Telas
![Tela principal](https://i.ibb.co/6XvZ0rC/tela-pergunta.png)
![Tela com o status das perguntas](https://i.ibb.co/MC9xkF3/tela-status.png)