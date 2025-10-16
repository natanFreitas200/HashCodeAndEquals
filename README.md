# HashCode e Equals em Java

Este projeto demonstra a implementação correta dos métodos `hashCode()` e `equals()` em Java, conceitos fundamentais para comparação de objetos e uso eficiente em estruturas de dados como `HashSet`, `HashMap` e outras coleções baseadas em hash.

## Sobre o Projeto

O projeto contém uma classe `Client` que exemplifica como implementar corretamente os métodos `hashCode()` e `equals()` seguindo as melhores práticas do Java. A aplicação demonstra a diferença entre:
- Comparação de referência (`==`)
- Comparação de conteúdo (`equals()`)
- Geração de código hash (`hashCode()`)

## Estrutura do Projeto

```
src/
├── application/
│   └── Main.java          # Classe principal com exemplos de uso
└── entities/
    └── Client.java        # Classe modelo com implementação de equals() e hashCode()
```

## Como Executar

### Pré-requisitos
- Java JDK 8 ou superior
- IDE Java (IntelliJ IDEA, Eclipse, VS Code, etc.) ou compilador Java

### Passos para execução

1. **Clone o repositório:**
   ```bash
   git clone https://github.com/natanFreitas200/HashCodeAndEquals.git
   cd HashCodeAndEquals
   ```

2. **Compile o projeto:**
   ```bash
   javac -d out src/application/Main.java src/entities/Client.java
   ```

3. **Execute a aplicação:**
   ```bash
   java -cp out application.Main
   ```

### Saída Esperada
```
[hashCode do client1]
[hashCode do client2]
true
false
```

## Conceitos Demonstrados

### Contrato equals() e hashCode()

A implementação na classe `Client` segue as regras fundamentais:

1. **Reflexividade:** `x.equals(x)` deve retornar `true`
2. **Simetria:** `x.equals(y)` deve retornar `true` se e somente se `y.equals(x)` retornar `true`
3. **Transitividade:** Se `x.equals(y)` e `y.equals(z)` retornam `true`, então `x.equals(z)` deve retornar `true`
4. **Consistência:** Múltiplas invocações devem retornar o mesmo resultado
5. **Contrato com hashCode():** Se dois objetos são iguais via `equals()`, devem ter o mesmo `hashCode()`

### Implementação na Classe Client

```java
@Override
public boolean equals(Object o) {
    if (this == o) return true;                           // Verificação de referência
    if (o == null || getClass() != o.getClass()) return false;  // Verificação de tipo
    Client client = (Client) o;
    return name.equals(client.name) && email.equals(client.email);  // Comparação de campos
}

@Override
public int hashCode() {
    return Objects.hash(name, email);  // Hash baseado nos mesmos campos do equals()
}
```

## Conceitos-Chave

| Método | Propósito | Quando Usar |
|--------|-----------|-------------|
| `equals()` | Comparar conteúdo de objetos | Verificar se dois objetos são "logicamente iguais" |
| `hashCode()` | Gerar código hash | Uso em HashMap, HashSet, Hashtable |
| `==` | Comparar referências | Verificar se duas variáveis apontam para o mesmo objeto |

## Casos de Uso Práticos

Este padrão é essencial quando você precisa:
- Armazenar objetos em `HashSet` ou usar como chave em `HashMap`
- Comparar objetos de forma lógica (não por referência)
- Implementar objetos de valor (Value Objects)
- Trabalhar com coleções que dependem de igualdade

## Pontos Importantes

1. **Sempre implemente ambos:** Se você sobrescrever `equals()`, deve também sobrescrever `hashCode()`
2. **Use os mesmos campos:** Os campos usados em `equals()` devem ser os mesmos usados em `hashCode()`
3. **Considere imutabilidade:** Campos usados em equals/hashCode idealmente devem ser imutáveis
4. **Performance:** `hashCode()` deve ser eficiente, pois é chamado frequentemente em estruturas hash

## Contribuindo

Contribuições são bem-vindas! Sinta-se à vontade para:
- Reportar bugs
- Sugerir melhorias
- Adicionar exemplos
- Melhorar a documentação


