## Introdução

O objetivo deste relatório é analisar os processos de verificação e validação (V & V) e ainda algumas características pertinentes ao tema. 
O relatório estará dividido em 4 partes: 
* Numa primeira fase, irá se explorar o grua de testabilidade do software, analisando os processos de verificação e validação assim como a contrabilidade, observabilidade, Isolabilidade, Separação de Funcionalidades, Documentação, Heterogeneidade das tecnologias utilizadas, etc... 
* Na segunda fase será apresentado estatísticas de Testes efetuados, no que diz respeito ao número de testes, cobertura, entre outros aspetos; 
*  Na terceira parte, haverá uma analise de um bug report resolvido; 
*  Por fim, uma pequena critica sobre as técnicas utilizadas.

## Testabilidade do software

Nesta secção iremos falar sobre o grau de testabilidade ao analisar os processos de verificação e validação.

#### Grau de testabilidade

Sendo o Geoserver um software de elevada complexidade é impossível testar método a método à procura de bugs, como tal existem 3 tipos de testes Unit, Integration/Mock, System, que serão aprofundados mais à frente. Os teste Unit como o próprio nome indica, testa cada método criado, no entanto nem sempre é possível fazê-lo, visto que há muitos módulos incorporados, como tal existem os "integration tests" utilizados para testar módulos com dependências de outros.  

#### Isolabilidade 
Uma grande dificuldade em programas complexos como este é tentar isolar cada componente para testar, de forma a que o teste não dependa do resultado de outra componente que não está a ser testada diretamente mas que influência o resultado. É para isso que serve os testes de integração/mock, isto é, funções que substituirão funções reais definidas em módulos dos quais essa unidade depende. Para tal existe uma framework chamada MockRunner e uma biblioteca EasyMock como será explicado logo à frente.

#### Controlabilidade
Como referido anteriormente, os testes mais importantes neste software são o Unit, Integration/Mock e System Tests. 
Começando pelos testes unitários, o Geoserver utiliza uma ferramenta de testes automáticos chamada Jenkins. Esta ferramenta permite efetuar testes unitários em JUnit e  XMLUnit. Contém, também, uma página de estatísticas, que ilustra os resultados obtidos (ex: quantidade e cobertura dos testes). O testes são criados pelo desenvolvedor do software. Esta ferramenta oferece: 
*  "Checkstyle - Confere o estilo do código para verificar se as mesmas convenções são usadas em todos os sítios"; 
*  "FindBugs - Procura fragmentos de código cuja estrutura possa induzir a bugs ou outros erros"; 
*  "Open Tasks - Procura comentários com "TODO" no código para listar a quantidade de tarefas por fazer"; 
*  "Code Coverage - Quantidade de linhas de código cobertas pelos testes". 

Este teste é particularmente importante, visto que os testes unitários são realizados sobre métodos, é uma mais valia para o Geoserver, visto que este é programado numa linguagem orientada por objetos,  permitindo assim um maior controlo sobre o que está a ser testado.  
O segundo tipo de testes mencionado, são os testes de integração, que fazem uso de ferramentas como MockRunner(framework) e EasyMock(library). Estes testes são utilizados quando uma componente necessita de interagir com outra para operar. No Geoserver estes testes  simulam dependências entre as componentes ao cria-las diretamente ou através da biblioteca "Easy Mock". 

O último tipo de testes são os "System Tests". Testam uma componente ou um conjunto de componentes com o sistema em execução. No Geoserver, estes são os testes que criam um sistema completamente funcional, incluindo um diretorio/configuração data. 
"System tests" são o tipo mais comum de casos de testes no GeoServer, principalmente por serem testes fáceis de escrever. No entanto, há uma desvantagem de "perfomance", devido ao facto de estes testes serem bastante exigentes. O sistema de testes do  GeoServer  oferece um sistema completamente funcional. Criar este sistema é uma operação expendiosa e deve ser utilizada em último recurso.  
No GeoServer este testes "extend" da class "org.geoserver.test.GeoServerSystemTest". O ciclo de vida do sistema segue as seguintes etapas: 
<p>1. System initialization </p>
<p>2. System creation </p>
<p>3. Test execution </p>
<p>4. System destruction </p>

#### Observabilidade
O GeoServer utiliza ferramentas de testes unitários e integração, assim como, de cariz dinâmico, ferramentas e bibliotecas para "System Tests". 
Em relação aos testes, é usada uma ferramenta chamada Jenkins, através da qual é possível efetuar testes unitários em JUnit. Assim é possível acompanhar as estatísticas de cada tentativa de pull  request. 
Como já dito anteriormente as ferramentas usadas no Geoserver são: 

__JUnit__ 
<p> Junit framework is the primary test library used in GeoServer. The current version used is Junit 4.11. While it is possible to continue to write JUnit 3.x style tests with JUnit 4, new tests should be written in the JUnit4 style with annotations. </p>  

__XMLUnit__
<p> The XMLUnit library provides a convenient way to make test assertions about the structure of XML documents. Since many components and services in GeoServer output XML, XMLUnit is a very useful library. </p>  

__MockRunner__ 
<p> The MockRunner framework provides a set of classes that implement the various interfaces of the J2EE and Java Servlet apis. It is typically used to create HttpServletRequest , HttpServletResponse, etc... objects for testing servlet based components. Current version: 0.3.6 </p>  

__EasyMock__ 
<p> The Easymock library is a mocking framework that is used to simulate various objects without actually creating a real version of them. This is an extremely useful tool when developing unit tests for a component A, that requires component B when component B may not be so easy to create from scratch. 
Current version: 2.5.2 </p> 

No entanto, é importante ainda salientar, a classe de testes que o GeoServer possui, como explicado anterior.


#### Separação de Funcionalidades 
Ao analisarmos o GeoServer é possível observar que cada funcionalidade está organizada corretamente no módulo correspondente. Cada um dos módulos principais possui um conjunto de tarefas da qual é responsável. Outra coisa importante verificada, é que cada módulo tem uma pasta dedicada a testes, sejam eles teste unitários ou "system tests". 
De um nível mais geral, o GeoServer ainda possui 3 versões, com estrutura exatamente igual. A atual, utilizada pelo consumidor, a próxima a ser lançada (e que está em fase de testes) e a que está a começar a ser desenvolvida, como foi explicito em relatórios anteriores.

#### Inteligibilidade
O GeoServer tem na sua composição uma pasta chamada doc. Esta pasta contém fontes de guiões para o utilizador e desenvolvedor, visto que é possível ao utilizador "programar" as suas funcionalidades. No entanto, torna-se um pouco complicado para qualquer desenvolvedor iniciar-se no GeoServer, visto que apenas funções simples estão bem comentadas, grandes módulos nota-se a falta de documentação, que normalmente é um link para uma documentação bastante redundante e exaustiva. O GeoServer usa o JIRA para listar os problemas. Nova documentação é tratada como parte do código, para que quem queira submeter algo (patches etc) possa usar um pull request ou afixar um problema com o JIRA juntamente com conteúdo sobre o problema. 



#### Heterogeneidade  

O GeoServer é um projeto com grande heterogeneidade, visto que usa várias tecnologias externas para executar. Algumas dessas bibliotecas que achamos pertinentes serão aqui identificadas:  
 
__Findbugs__  
<p> Findbugs is a static analysis tool for Java bytecode. It operates by searching compiled Java code for common programming errors such as dereferencing null pointers. In GeoServer we use Findbugs to augment the unit test suite. </p>
__GeoTools__   
<p>GeoTools is an open source Java library that provides tools for geospatial data. </p>
__Web Feature Service__ 
<p>In computing, the Open Geospatial Consortium Web Feature Service Interface Standard (WFS) provides aninterface allowing requests for geographical features across the web using platform-independent calls </p>
__GeoWebCache__ 
<p>GeoWebCache is a Java web application used to cache map tiles coming from a variety of sources such as OGC Web Map Service (WMS).</p> 


## Estatísticas de Teste

Basta ir à pagina do Jenkins do Geoserver e ver os  testes unitários....

## Bug Report Resolvido

Um pequeno exemplo com informação sobre o problema, resolução e pull request do mesmo....


## Critica




















































Glossário


JUnit:
•	 JUnit framework is the primary test library used in GeoServer. The current version used is Junit 4.11. While it is possible to continue to write JUnit 3.x style tests with JUnit 4, new tests should be written in the JUnit4 style with annotations.
XMLUnit:
•	The XMLUnit library provides a convenient way to make test assertions about the structure of XML documents. Since many components and services in GeoServer output XML, XMLUnit is a very useful library.
MockRunner
The MockRunner framework provides a set of classes that implement the various interfaces of the J2EE and Java Servlet apis. It is typically used to create HttpServletRequest , HttpServletResponse, etc... objects for testing servlet based components.
Current version: 0.3.6
EasyMock
The EasyMock library is a mocking framework that is used to simulate various objects without actually creating a real version of them. This is an extremely useful tool when developing unit tests for a component A, that requires component B when component B may not be so easy to create from scratch.
Current version: 2.5.2
