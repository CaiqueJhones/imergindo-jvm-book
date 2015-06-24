#### Classes após compilação


Uma vez falando dos **bytecodes** é interessantes “puxar o gancho” e falar como fica uma classe após sua compilação. Como já foi dito após a compilação é gerado um **bytecode**, cujo arquivo possui a extensão .class, e cada arquivo representa apenas uma classe. Cada arquivo possui as seguintes características:

 
* Um número mágico em hexadecimal definindo que essa clase é um .class o valor é **0xCAFEBABE**

* O maior e menor número da versão do arquivo class que juntos definem a versão do arquivo, ou seja, JVM antes rodar precisa verificar se a versão V que ela pode executar estar entre: Menor Versão<V< Maior Versão.

* **access_flags**: Essa flag indica o tipo de encapsulamento da classe, métodos e de suas propriedades os flags podem ser:


* **ACC_PUBLIC**: flag método, atributos públicos
* **ACC_PRIVATE**: flag para privados
* **ACC_PROTECTED**: protected
* **ACC_STATIC**: estático
* **ACC_FINAL**: final
* **ACC_SYNCHRONIZED**: indica um método sincronizado
* **ACC_BRIDGE**: indica que o método foi gerado pelo compilador
* **ACC_VARARGS**: indica que é varags 
* **ACC_NATIVE**: nativo
* **ACC_ABSTRACT**: abstrato
* **ACC_STRICT**: indica que o método é strict
* **ACC_SYNTHETIC**: indica que o método não é “original”


. 
* **this_class**: o valor da corrente classe deve ter um índice válido na constant pool
 
* **super_class**: as informações da superclasse devem estar dentro e pode ocupar o índice zero ou não, se ocupar o índice zero essa classe é o java.lang.Object, a única classe que não possui pai, do contrário terá que ser um índice válido e ter informações que apontam para a classe pai. As informações da classe é definida pelo seu nome com o seu caminho, por exemplo, a nome da String seria java/lang/String.

* **constant pool**: O constant pool é uma estrutura de tabela que contém o nome das classes, interfaces, métodos, atributos e outras informações das classes. Para guardar essas informações existem dois registadores par cada informação importante: O vetor coma s informações da classe, método, ou atributos e o seu contador ou índice que funciona como limitador do vetor. Esse é o caso das interfaces que a classe implementa, atributos, métodos que possuem seus respectivos vetor e índices.

* As descrições dos atributos ou dos parâmetros em um método quanto ao seu tipo é definido a seguir:

  * B byte signed byte 
  * C char 
  * D double 
  * F float 
  * I int 
  * J long 
  * L Classname ; referência 
  * S short
  * Z boolean 
  * [ referência de um vetor 
  * [[ referência de uma matriz 


Assim, por exemplo: `double dobro(double d)` é igual  `(D)D` e `Double dobro(Double d)` é `(Ljava/lang/Double;)Ljava/lang/Double`.

Dentro da constant pool cada informação possui o seu primeiro byte que indica o seu tipo de informação:


  * CONSTANT_Class 7 
  * CONSTANT_Fieldref 9 
  * CONSTANT_Methodref 10 
  * CONSTANT_InterfaceMethodref 11 
  * CONSTANT_String 8 
  * CONSTANT_Integer 3 
  * CONSTANT_Float 4 
  * CONSTANT_Long 5 
  * CONSTANT_Double 6 
  * CONSTANT_NameAndType 12 
  * CONSTANT_Utf8 1 
  * CONSTANT_MethodHandle 15 
  * CONSTANT_MethodType 16 
  * CONSTANT_InvokeDynamic 18 




**StackMapTable**: é composto de stackmapframe e tem o objetivo de verificações para o bytecode

Para auxiliar a depuração na linguagem Java existem algumas informações para depurar o código essas variáveis são: LocalVariableTable e LocalVariableTypeTable que define as informações das variáveis locais para o debug e LineNumberTable define a parte do bytecode e sua correspondente linha de código.
Para as anotações exitem: `RuntimeVisibleAnnotations`, `RuntimeInvisibleAnnotations`, `RuntimeVisibleParameterAnnotations`, `RuntimeInvisibleParameterAnnotations` que contém informações das anotações quanto a sua visibilidade em tempo de execução aos atributos e métodos ou não, existem essas mesmas informações para os parâmetros quanto as suas visibilidades. `AnnotationDefault` define as informações dentro das anotações.


O contador da consant pool possui 16 bits, ou seja, ele só pode conter 2¹⁶=65535 elementos, esse mesmo número vale para o número de métodos, atributos, interfaces implementadas, variáveis locais, pilha de operações (sendo que para esses dois últimos o longo e o double ocupam dois espaços), o nome do método ou atributo. O número de dimensões de uma matriz é 255 o mesmo número vale para a quantidade de parâmetros, caso não seja um método estático deve-se incluir a instância.
	
Com o objetivo de pôr em prática e visualizar esses bytescodes, será demonstrado um simples código e o seu respectivo bytecode.