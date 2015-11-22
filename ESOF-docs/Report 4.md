## Introdução

O objetivo deste relatório é analisar os processos de verificação e validação (V & V) e ainda algumas características pertinentes ao tema.
O relatório estará dividido em 3 partes:
•	Numa primeira fase, irá se explorar o grua de testabilidade do software, analisando os processos de verificação e validação assim como a contrabilidade, observabilidade, Isolabilidade, Separação de Responsabilidades, Documentação, Heterogeneidade das tecnologias utilizadas, etc...
•	Na segunda fase será apresentado estatísticas de Testes efectuados, no que diz respeito ao número de testes, cobertura, entre outros apetos;
•	Por fim, haverá a analise de um bug report resolvido

## Testabilidade do software

Nesta secção iremos falar sobre o grau de testabilidade ao analisar os processos de verificação e validação.

#### Grau de testabilidade (completo)

Sendo o Geoserver um software de elevada complexidade é impossível testar método a método à procura de bugs, como tal existem 3 tipos de testes Unit, Integration/Mock, System, que serão aprofundados mais à frente. Os teste Unit como o próprio nome indica, testam cada método criado, no entanto nem sempre é possível fazê-lo, visto que há muitos módulos incorporados, como tal existem os "integration tests" utilizados para testar código com dependências de outro.

#### Isolabilidade (completo)
Uma grande dificuldade em programas complexos como este é tentar isolar cada componente para testar, de forma a que o teste não dependa do resultado de outra componente que não está a ser testada diretamente mas que influência o resultado. É para isso que serve os testes de integração/mock, isto é, funções que substituirão funções reais definidas em módulos dos quais essa unidade depende. Para tal existe uma framework chamada MockRunner e uma biblioteca EasyMock como será explicado logo à frente.

#### Controlabilidade (completo)
Como referido anteriormente, os testes mais importantes neste software são o Unit, Integration/Mock, System  tests.
Começando pelos testes unitários, o Geoserver utiliza uma ferramenta de testes automáticos chamada Jenkins. Esta ferramenta permite efectuar testes unitários em JUnit e  XMLUnit. Contem, também, uma pagina de estatísticas, que ilustra os resultados obtidos (ex: quantidade e cobertura dos testes). O testes são criado pelo desenvolvedor do software. Esta ferramenta oferece:
•	"Checkstyle - Confere o estilo do código para verificar se as mesmas convenções são usadas em todos os sítios";
•	"FindBugs - Procura fragmentos de código cuja estrutura possa induzir a bugs ou outros erros";
•	"Open Tasks - Procura comentários com "TODO" no código para listar a quantidade de tarefas por fazer";
•	"Code Coverage - Quantidade de linhas de código cobertas pelos testes".
Este teste é particularmente importante, visto que os testes unitários são realizados sobre métodos, é uma mais valia para o Geoserver, visto que este é programado numa linguagem orientada por objetos,  permitindo assim um maior controlo sobre o que está a ser testado.
O segundo tipo de testes mencionado, são os testes de integração, que fazem uso de ferramentas como MockRunner(frameWork) e EasyMock(library). Estes testes são utilizados quando uma componente necessita de interagir com outra para operar. No Geoserver estes testes que de alguma forma simulam dependencias entre as componentes ao cria-las diretamente ou através da biblioteca "Easy Mock".
O último tipo de testes são os "System". Tests that exercise a component or set of components by testing it in a fully running system. In GeoServer these are tests that create a fully functional GeoServer system, including a data directory/configuration and a spring context.
System tests are the most common type of test case in GeoServer, primarily because they are the easiest tests to write. However they come with a cost of performance. The GeoServer system test framework provides a fully functional GeoServer system. Creating this system is an expensive operation so a full system test should be used only as a last resort. Developers are encouraged to consider a straight unit or mock tests before resorting to a full system test.
In GeoServer system tests extend from the org.geoserver.test.GeoServerSystemTest class. The general lifecycle of a system test goes through the following states:
1.	System initialization
2.	System creation
3.	Test execution
4.	System destruction
Phases 1 and 2 are referred to as the setup phase. It is during this phase that two main operations are performed. The first is the creation of the GeoServer data directory on disk. The second is the creation of the spring application context.

#### Observabilidade

Como já dito anteriormente as ferramentas usadas no Geoserver são:

* __JUnit__:

	 JUnit framework is the primary test library used in GeoServer. The current version used is Junit 4.11. While it is possible to continue to write JUnit 3.x style tests with JUnit 4, new tests should be written in the JUnit4 style with annotations.
* __XMLUnit__:

	The XMLUnit library provides a convenient way to make test assertions about the structure of XML documents. Since many components and services in GeoServer output XML, XMLUnit is a very useful library.

* __MockRunner__:

	The MockRunner framework provides a set of classes that implement the various interfaces of the J2EE and Java Servlet apis. It is typically used to create HttpServletRequest , HttpServletResponse, etc... objects for testing servlet based components.
  Current version: 0.3.6

* __EasyMock__

 The EasyMock library is a mocking framework that is used to simulate various objects without actually creating a real version of them. This is an extremely useful tool when developing unit tests for a component A, that requires component B when component B may not be so easy to create from scratch.
	Current version: 2.5.2


#### Separação de Funcionalidades --> como está organizada cada componente, se cada funcionalidade está implementada na componente a que diz respeito, etc....

#### Inteligibilidade -- > como está a documentação e critica...



#### Heterogeneidade -> falar sobre as bibliotecas utilizadas e critica...

O GeoServer é um projeto com grande heterogeneidade, visto que usa várias tecnologias externas para executar. As principais caracteristicas identificadas foram:

* Findbugs:

  Findbugs is a static analysis tool for Java bytecode. It operates by searching compiled Java code for common programming errors such as dereferencing null pointers. In GeoServer we use Findbugs to augment the unit test suite.



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
