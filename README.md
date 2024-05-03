# Implementação de Padrões de Projeto
**Introdução**:
Neste projeto, demonstraremos alguns padrões importantes de padrões de projeto, distribuídos por um padrão de cada categoria: criacional, estrutural e comportamental.

### Padrões Criacionais:

#### Factory Method:

**Para o que serve:**
O padrão Factory Method é usado para definir uma interface para criar um objeto, mas permite que as subclasses alterem o tipo de objetos que serão criados.

**Problema que resolve:**
Permite criar objetos sem especificar a classe exata do objeto que será criado.

**Solução:**
A solução é definir uma interface para criar objetos em uma superclasse, mas permitir que as subclasses alterem o tipo de objetos que serão criados.

**Diagrama UML:**
```
             +------------------+
             |     Creator      |
             +------------------+
             | +factoryMethod() |
             +--------+---------+
                      |
                      v
              +-------+-------+
              |   Concrete    |
              |    Creator    |
              +---------------+
              | +factoryMethod|
              +--------+------+
                       |
                       v
            +----------+----------+
            |     ProductFactory   |
            +----------------------+
            | +createProduct()     |
            +----------------------+
```

**Código:**
```python
from abc import ABC, abstractmethod

class Product(ABC):
    @abstractmethod
    def operation(self):
        pass

class ConcreteProduct(Product):
    def operation(self):
        return "ConcreteProduct operation"

class Creator(ABC):
    @abstractmethod
    def factory_method(self):
        pass

    def some_operation(self):
        product = self.factory_method()
        result = f"Creator: {product.operation()}"
        return result

class ConcreteCreator(Creator):
    def factory_method(self):
        return ConcreteProduct()

# Exemplo de uso
creator = ConcreteCreator()
result = creator.some_operation()
print(result)  # Saída: "Creator: ConcreteProduct operation"
```

### Padrões Estruturais:

#### Adapter:

**Para o que serve:**
O padrão Adapter é usado para permitir que objetos com interfaces incompatíveis trabalhem juntos.

**Problema que resolve:**
Permite a comunicação entre duas interfaces diferentes que normalmente não seriam compatíveis.

**Solução:**
O Adapter envolve um objeto com uma interface diferente, fornecendo uma maneira flexível de estender funcionalidades.

**Diagrama UML:**
```
              +--------------+               +------------+
              |    Target    |<--------------|   Adapter  |
              +--------------+               +------------+
              | +request()   |               | +specific()|
              +------+-------+               +------------+
                     |
                     v
           +---------+---------+
           |      Adaptee      |
           +-------------------+
           | +specificRequest()|
           +-------------------+
```

**Código:**
```python
class Target:
    def request(self):
        return "Target: The default target's behavior."

class Adaptee:
    def specific_request(self):
        return ".eetpadA eht fo roivaheb laicepS"

class Adapter(Target):
    def __init__(self, adaptee):
        self.adaptee = adaptee

    def request(self):
        return f"Adapter: (TRANSLATED) {self.adaptee.specific_request()[::-1]}"

# Exemplo de uso
adaptee = Adaptee()
adapter = Adapter(adaptee)
result = adapter.request()
print(result)  # Saída: "Adapter: (TRANSLATED) Special behavior of the Adaptee."
```

### Padrões Comportamentais:

#### Strategy:

**Para o que serve:**
O padrão Strategy é usado para definir uma família de algoritmos, encapsular cada um deles e torná-los intercambiáveis.

**Problema que resolve:**
Permite que o algoritmo varie independentemente dos clientes que o usam.

**Solução:**
A solução é definir uma família de algoritmos, encapsulando cada um deles e tornando-os intercambiáveis.

**Diagrama UML:**
```
              +---------------------+
              |       Context       |
              +---------------------+
              | +strategy: Strategy |
              +---------------------+
                         |
                         v
           +-------------+-------------+
           |          Strategy          |
           +----------------------------+
           | +algorithm_interface()     |
           +----------------------------+
                     /|\
                      |
          +-----------+-----------+
          |       Concrete       |
          |       Strategy       |
          +----------------------+
          | +algorithm_interface()|
          +----------------------+
```

**Código:**
```python
from abc import ABC, abstractmethod

class Strategy(ABC):
    @abstractmethod
    def algorithm_interface(self):
        pass

class ConcreteStrategyA(Strategy):
    def algorithm_interface(self):
        return "ConcreteStrategyA algorithm"

class ConcreteStrategyB(Strategy):
    def algorithm_interface(self):
        return "ConcreteStrategyB algorithm"

class Context:
    def __init__(self, strategy):
        self.strategy = strategy

    def context_interface(self):
        return self.strategy.algorithm_interface()

# Exemplo de uso
context = Context(ConcreteStrategyA())
result = context.context_interface()
print(result)  # Saída: "ConcreteStrategyA algorithm"
```
