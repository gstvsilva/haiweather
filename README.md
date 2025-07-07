

# Experiência com o Google AI Studio

Tendo em vista algumas das orientações dos módulos 4 e 5 do curso de Gen AI, decidi recorrer ao Google AI Studio para testar principalmente a abordagem Chain of Thought (CoT).

Assim, optei por solicitar a ele a implementação de um site simples, “a princípio” de maneira totalmente leiga (sem fornecer a ele insights de codificação), dividindo sua evolução em duas etapas:


## Primeira etapa - definição da funcionalidade básica e do layout

Inicialmente, os prompts que inseri foram basicamente:

<pre>
construa um site que realize a consulta a uma API de previsão do tempo gratuita, que me permita obter dados de temperatura, sensação térmica e clima.

no canto superior esquerdo da tela, quero visualizar estas informações de forma destacada.

abaixo desta área, desejo visualizar dois containers também com dados meteorológicos, exibindo respectivamente:

- dados das cinco últimas horas;
- dados das próximas 24 horas. 
</pre>

Os resultados disso foram:

### API implementada com problemas: 
A IA buscou e implementou uma API bastante conhecida, mas apresentou diversos problemas na geração do código fonte. A URL apresentava problemas de formatação graves e, apesar da IA identificar o problema e retornar respostas claras indicando isso, quando eu pedia pra ela gerar todo o código da página novamente, o problema retornava.

Neste ponto, a IA passou a me retornar respostas como: 

<pre>
You have correctly identified a persistent and bizarre error in my output. The problem is with me, the AI model. For some reason, my generation process is corrupting the specific string &current= into ¤t=. This is a model-level glitch, and I am deeply sorry for the frustration it has caused. Your persistence has been crucial in helping me recognize this internal fault.”
</pre>

Assim, tive que ser bastante insistente sobre o ponto em que ela estava errando, e sugerir que todo novo código gerado deveria passar por um teste do endpoint consumido (pois a partir de certo momento ela passava a gerar endpoints até mesmo com parâmetros inválidos, “inventados”)

### Layout bastante problemático: 
Mesmo especificando de maneira leiga que os containers não deveriam extrapolar a largura da tela, a IA respondia positivamente, alegando que entendia minha solicitação, mas não gerava um código adequado. Por várias vezes tentei não indicar de maneira explícita a ela como resolver o problema, através da ativação do scroll horizontal e da determinação do max-width dos elementos, mas só quando passei a utilizar prompts com dados mais técnicos ela entregou o resultado esperado.


## Segunda etapa - exibição de conteúdos de acordo com a temperatura atual retornada pela API

Depois disso, inseri alguns prompts (dando exemplos de comportamento, como podem verificar), como:

<pre>
Defina o background da página partindo de cinza e indo até laranja, onde a intensidade da cor deve considerar a temperatura atual retornada pela API. Por exemplo, a temperatura 0 deve exibir o cinza escuro, enquanto a temperatura 40 deve exibir o laranja intenso
</pre>

<pre>
gere uma lista de 15 haicais para cada temperatura, variando de 0 a 40, onde cada um dos respectivos haicais deve ter relação com a temperatura em questão. Por exemplo, um haicai de temperatura 0 deve se relacionar ao frio intenso, enquanto um haicai de temperatura 40 deve se relacionar ao calor intenso. Temperaturas abaixo de 0 devem exibir os haicais da temperatura 0, e temperaturas acima de 40 devem exibir os haicais da temperatura 40
</pre>

Inicialmente este ponto funcionou bastante bem, porém comecei a ter vários problemas na geração do código completo da página. Acredito que isso tenha ocorrido por conta do longo histórico que CoT estava gerando, pois a IA passou a se perder em vários momentos, como por exemplo:

- Remoção indevida de código: a IA passou a gerar código incompleto, muitas vezes removendo o array de haicais, mesmo quando eu dizia explicitamente que ela não deveria fazer isso.

- Problema na organização do código: muitas vezes escrevi prompts claros sobre como o código gerado deveria ser mais amigável, pois muitos métodos acabavam sendo escritos in line. Neste ponto a IA se confundia muito, estragando o layout já consolidado, por exemplo.


## Conclusão:

- Acredito que o Google IA Studio consiga resultados mais acurados caso receba mais recursos nas etapas iniciais e não precise de tantas interações sobre um mesmo problema. No final, acabei não obtendo o código da maneira que eu desejava (podem verificar que sua formatação não seguiu um padrão), apesar de ele estar funcionando;

- A ideia de que a ferramenta pode partir do zero e auxiliar plenamente um leigo no assunto, ao meu ver, não se concretizou. Precisei “opinar” de maneira técnica muito mais do que eu esperava;

- Em vários momentos a IA agia de maneira que eu já havia especificado veementemente que não queria, como no caso da organização do código. Por diversas vezes deixei muito claro que não queria separar as responsabilidades do código em arquivos distintos (pois realizar imports gerava problemas de CORS), mas era induzido a isso constantemente;

- ao final, o esforço da IA parecia mais direcionado a se desculpar pelas falhas de maneiras diferentes do que conseguir seguir minhas orientações. :p 
