# Sintaxe e observações

### Tipos de dados em C:
- Tipos primitivos:
    - char:	caracter
    - int: inteiro
    - float:	real de precisão simples
    - double: real de precisao dupla
    - void:	vazio (sem valor)

### Entrada e saída
- import padrão: #include <stdio.h> ---> input e output
```c
printf("Para printar uma variavel basta usar plaholder: %s, %d, %f, %c", nome_da_variavel, nome_da_variavel, nome_da_variavel, nome_da_variavel) // output
scanf("tipo lido: %s, %d, %f, %c", &nome_da_variavel, &nome_da_variavel, &nome_da_variavel, &nome_da_variavel)
gets()
//fabs(num) --> valor absoluto

//while(1) --> equivalente ao while(True)
```
### Operadores
```c
// ? --> então
// nota = ((p1 > p2 ? p1:p2) + p3)/3; --> p1 é maior de p2 então ...
```
### Ponteiros
- armazena valores de endereços de memória
- é tipado: reservo um endereço prepardo para um tipo de dado
- Declaração:
  - ***"int *p - float *p"***
  - mais de um ponteiro na mesma linha: ***"int *p, *q"***
- Operadores com Ponteiros: & (endereço de memória), * (conteúdo do endereço de memória)
- Exemplo:
```c
int a;
int *p; // criando o ponteiro p
a = 5
p = &a; // atribuindo ao ponteiro p o endereço de memória de a
// p aponta para o endereço de a
*p = 6; // p atribui ao conteúdo de a o inteiro 6
```
- Ponteiros como parâmetros na função:
```c
void somaprod (int a, int b, int* p, int* q){ // são passados como parâmetros os ponteiros *p e *q
    *p = a+b; // é atribuído ao conteúdo do ponteiro *p a soma de a e b
    *q = a*b; // é atribuído ao conteúdo do ponteiro *q o prod de a e b
}
int main(void){
    int s,p;
    somaprod(3,5, &s, &p); // é passado como parâmetro para os ponteiros p e q o endereço de memória de s e p
    // portanto, p --> s e q --> p
    printf("Soma = %d - Prod = %d\n", s, p)
    return 0
}

```
