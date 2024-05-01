

---

# Implementação de Padrões de Projeto

## Introdução:
Neste projeto, demonstraremos alguns padrões importantes de padrões de projeto, distribuídos por um padrão de cada categoria: criacional, estrutural e comportamental.

## Padrões Criacionais:
### Factory Method:
#### Para o que serve:
O padrão Factory Method é usado para definir uma interface para criar um objeto, mas permite que as subclasses alterem o tipo de objetos que serão criados.

#### Problema que resolve:
Permite criar objetos sem especificar a classe exata do objeto que será criado.

#### Solução:
A solução é definir uma interface para criar objetos em uma superclasse, mas permitir que as subclasses alterem o tipo de objetos que serão criados.

#### Diagrama UML:
```plaintext
                      +--------------+
                      |   Creator    |
                      +--------------+
                      | +factoryMethod()|
                      +------+-------+
                             |
                  +----------+-----------+
                  |                      |
          +--------------+       +--------------+
          |   Concrete   |       |   Concrete   |
          |   Creator    |       |   Creator    |
          +--------------+       +--------------+
          |   +factoryMethod()|   |   +factoryMethod()|
          +------------------+   +------------------+
```

#### Código:

```java
public abstract class Creator {
    public abstract Product factoryMethod();
}

public class ConcreteCreator extends Creator {
    @Override
    public Product factoryMethod() {
        return new ConcreteProduct();
    }
}

public interface Product {
    void operation();
}

public class ConcreteProduct implements Product {
    @Override
    public void operation() {
        System.out.println("Operation implemented in ConcreteProduct");
    }
}
```

## Padrões Estruturais:
### Adapter:
#### Para o que serve:
O padrão Adapter é usado para permitir que objetos com interfaces incompatíveis trabalhem juntos.

#### Problema que resolve:
Permite a comunicação entre duas interfaces diferentes que normalmente não seriam compatíveis.

#### Solução:
O Adapter envolve um objeto com uma interface diferente, fornecendo uma maneira flexível de estender funcionalidades.

#### Diagrama UML:
```plaintext
                      +--------------+
                      |    Target    |
                      +--------------+
                      | +request()   |
                      +------+-------+
                             |
                  +----------+-----------+
                  |                      |
          +--------------+       +----------------+
          |    Adapter   |       |   Adaptee      |
          +--------------+       +----------------+
          | -adaptee: Adaptee |   | +specificRequest()|
          +------------------+   +------------------+
                  |                      |
                  |  +request()          |
                  +----------------------+
```

#### Código:

```java
public interface Target {
    void request();
}

public class Adapter implements Target {
    private Adaptee adaptee;

    public Adapter(Adaptee adaptee) {
        this.adaptee = adaptee;
    }

    @Override
    public void request() {
        adaptee.specificRequest();
    }
}

public class Adaptee {
    public void specificRequest() {
        System.out.println("Specific request in Adaptee");
    }
}
```

## Padrões Comportamentais:
### Strategy:
#### Para o que serve:
O padrão Strategy é usado para definir uma família de algoritmos, encapsular cada um deles e torná-los intercambiáveis.

#### Problema que resolve:
Permite que o algoritmo varie independentemente dos clientes que o usam.

#### Solução:
A solução é definir uma família de algoritmos, encapsulando cada um deles e tornando-os intercambiáveis.

#### Diagrama UML:
```plaintext
                      +---------------------+
                      |      Context        |
                      +---------------------+
                      | -strategy: Strategy |
                      +---------------------+
                      | +contextInterface() |
                      +----------+----------+
                                 |
                 +---------------+--------------+
                 |                              |
          +---------+                   +---------+
          | Strategy|                   | Strategy|
          +---------+                   +---------+
          |+algorithm()|                |+algorithm()|
          +------------+                +------------+
```

#### Código:

```java
public interface Strategy {
    void algorithm();
}

public class ConcreteStrategyA implements Strategy {
    @Override
    public void algorithm() {
        System.out.println("Executing algorithm A");
    }
}

public class ConcreteStrategyB implements Strategy {
    @Override
    public void algorithm() {
        System.out.println("Executing algorithm B");
    }
}

public class Context {
    private Strategy strategy;

    public Context(Strategy strategy) {
        this.strategy = strategy;
    }

    public void contextInterface() {
        strategy.algorithm();
    }
}
```

--- 

