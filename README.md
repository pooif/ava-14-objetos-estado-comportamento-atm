# 1.5 // Objetos, Estado e Comportamento // ATM

Use este link do GitHub Classroom para ter sua cópia alterável deste repositório: <>

Implementar respeitando os fundamentos de Orientação a Objetos.

**Tópicos desta atividade:** abstrações, classes, objetos, construtores, validade, atributos, estado, comportamento, comandos e consultas, excepcionalidades e especificações.

---

Considere a especificação de um **Caixa Eletrônico** (Automatic Teller Machine - ATM) e um _software_ que opere no _hardware_, ou seja, as contas, cartões, senhas e outras informações bancárias são irrelevantes, importando apenas o tratamento do abastecimento de dinheiro físico (em espécie) do **ATM** e subsequentes retiradas.

Considere que o **ATM** têm 5 compartimentos internos (1 a 5) cada um com capacidade para até 100 cédulas de `R$ 5,00`, `R$ 10,00`, `R$ 20,00`, `R$ 50,00` e `R$ 100,00` respectivamente. Os vigilantes abastecem o **ATM** com cédulas, no limite de cada compartimento, rejeitando abastecimentos que excedem esse limite.

Os clientes fazem suas retiradas no **ATM**, sendo irrelevante a operação (saque conta corrente, poupança, empréstimo), bastanto apenas ter cédulas (dinheiro físico) disponível no **ATM** e sendo possível atender o valor informado _conforme a combinação disponível de cédulas_, isto é: se o cliente solicitar `R$ 60,00` o **ATM** pode entregar 3 cédulas de `R$ 20`, uma de `R$ 50,00` e uma de `R$ 10,00`.

Se, por exemplo, o **ATM** estiver abastecido apenas com cédulas de `R$ 50,00` e `R$ 100,00` ele não poderá atender à solicitação de retirada de `R$ 60,00`, rejeitando a mesma.

O algoritmo de retirada deve priorizar a saída de cédulas de maior valor. O **ATM** deve ter, ainda, uma interface para consultar o valor total e quantidade de cédulas de cada compartimento.

Dada essa especificação, a implementação deve aderir aos seguintes casos de teste que demonstram a  interação básica com o ATM e **devem ser introduzidos mais casos teste que realizem retiradas que combinem 3, 4 e 5 cédulas, válidas e inválidas.**


```java
ATM atm = new ATM();

// abastecendo com 20 notas de 100
atm.abastecer(33, 100);

// verificando a quantidade de cédulas de 100
System.out.println(atm.consultarQuantidade(100)); // 33

// espera-se 33 cédulas
System.out.println(atm.consultarQuantidade(100) == 33);

// espera-se nenhuma cédula de qualquer outro valor
System.out.println(atm.consultarQuantidade(5)); // 0
System.out.println(atm.consultarQuantidade(5) == 0);
System.out.println(atm.consultarQuantidade(50)); // 0
System.out.println(atm.consultarQuantidade(50) == 0);

// mesmo de cédulas que não existem
System.out.println(atm.consultarQuantidade(3)); // 0
System.out.println(atm.consultarQuantidade(3) == 0);

// abastecimento de cédulas não existentes são rejeitados
atm.abastecer(8, 3); // 8 cédulas de R$ 3,00
System.out.println(atm.consultarQuantidade(3) == 0);

// consultando o valor
System.out.println(atm.consultarValor()); // 33 * 100 = 3300 reais
System.out.println(atm.consultarValor() == 3300);

// retirada rejeitada
atm.retirar(350); // não há cédulas de R$ 50,00
System.out.println(atm.consultarQuantidade(100) == 33);
System.out.println(atm.consultarValor() == 3300);

// retirada válida
atm.retirar(300); // 3 cédulas de 100
System.out.println(atm.consultarQuantidade(100) == 30);
System.out.println(atm.consultarValor() == 3000);

// retirada rejeitada
atm.retirar(3100); // não há cédulas suficientes
System.out.println(atm.consultarQuantidade(100) == 30);
System.out.println(atm.consultarValor() == 3000);

// retirada válida
atm.retirar(3000); // vai esvaziar o ATM
System.out.println(atm.consultarQuantidade(100) == 0);
System.out.println(atm.consultarValor() == 0);

// abastecimento de R$ 50,00 e R$ 10,00
atm.abastecer(10, 10); // 10 cédulas de R$ 10,00
atm.abastecer(10, 50); // 10 cédulas de R$ 50,00
System.out.println(atm.consultarQuantidade(10) == 10);
System.out.println(atm.consultarQuantidade(50) == 10);
System.out.println(atm.consultarValor() == 600); // 10 * 10 + 10 * 50

// retirada prioriza cédulas de maior valor
atm.retirar(100); // retira 2 cédulas de R$ 50,00
System.out.println(atm.consultarQuantidade(10) == 10);
System.out.println(atm.consultarQuantidade(50) == 8);
System.out.println(atm.consultarValor() == 500); // 10 * 10 + 8 * 50

// retirada combinada
atm.retirar(90); // 1 cédula de R$ 50,00 e 4 cédulas de R$ 10,00
System.out.println(atm.consultarQuantidade(50) == 7);
System.out.println(atm.consultarQuantidade(10) == 6);
System.out.println(atm.consultarValor() == 410); // 6 * 10 + 7 * 50

// incluir casos de teste pessoais com retiradas
// quem combinam 3, 4 e 5 cédulas, válidas e inválidas
```

### Observações

1. Os compartimentos não devem permitir o acesso direto, em outras palavras, a quantidade de cédulas só pode ser alterada através de abastecimentos e retiradas;
2. Existem outras situações inválidas, seus testes não são obrigatórios na atividade, mas é um diferencial qualitativo se forem implementados;
3. Os casos de teste não podem ser alterados, mas outros podem ser adicionados. Fique a vontade para adicionar códigos que imprimem ou separam os testes, por exemplo.
