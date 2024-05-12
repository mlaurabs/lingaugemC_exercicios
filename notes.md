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
// CONTINUAR
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
### Vetor
- ***O tamnho do vetor é imutável***
- Guarda apenas ***um tipo de dado***
- Exemplo: "int vetor[10] --> vetor de ints com 10 itens"
- Declaração de mais de um vetor: "float v[5], a[10]"
- Estrutura do vetores --> "double b[5] = {}"
- Incializando um vetor já com os valores --> "double c[2] = {1.5, 3.5}"
  - ***OBS.: nesse caso, ao inciar com os valores, o tamanho pode estar implícito como double c[] = {itens}***
  - Incialização parcial: "você não precisar definir de primeira todos os valores que serão alocados no espaço de memória defindo"
**- Vetor com Ponteiros**
    - Atribuindo o endereço do vetor a uma variável do tipo ponteiro --> "int* u = v"
```c
float a[3] = {4.5,6.7,8.9};
float* b = a; // o ponteiro guarda o enderço do vetor de floats a
// se acessarmos b[0], estamos acessando o valor float 4.5 //alocado nesse mesmo endereço do vetor a
u[0] = 7.8 --> 4.5 passa a ser 7.8
u[1] = v[0] + 1  --> 6.7 passa a ser 7.8+1 =8.8
```

- Paramâmetros como ponteiros que guardam o endereço de um vetor
    - Exemplo:

```c 
float prod(int n, float* p){ // apenas acessar os valores do vetor através do ponteiro
    float resul = 1.0f;
    for(int i=0; i < n; i++){
        resul *= p[i];
    }
    return p
}

void popula(int n, float* p){
    for(int i =0; i < n; i++){
        scanf("%f", &p[i]);
    }
}

int main(){
    int n = 3;
    int v[n] = {5,4,8};
    float vet[n];
    produto = prod(n, v); // é passado o enderço de memória v
para a ponteiro função p
    // os valores do vetor são acessados pelo ponteiro
    popula(n, vet); // atribui valores ao vetor vet através do ponteiro
    return 0;
}
```
*s --> char * --> stirng

### Alocação Dinâmica
- alocação estática:
  - requisita espaço em memória em tempo de compilação
  - Ex: "in vetor[10]"
- alocaçã dinâmica:
  - requisita espaço em memória em tempo de execução
  - tratamento de erro: exit()
    - aborta o programa
  - função malloc()
    - reserva em memória uma array de bytes
    - retorna um ponteiro genérico --> void*
    - retorna NULL, caso haja algum erro. Ex.: não há memória sufuciente no sistema
```c
#define TAM 10
//alocando vetor para 10 inteiros dinamicamente
int* v = (int*) malloc(TAM*sizeof(int)) //sizeof() --> retona o tamnho em bytes de um tipo de dado
// desta forma, o ponteiro v aponta para a memória alocada para um vetor de 10 inteiros
// é apenas um ponteiro para um vetor qualquer
// a memória alocada permanece reservada até uma liberação explícita ou até o programa terminar-
```

### Leitura de Arquivos
%c -->
%s --> pula espaços brancos
%[aA] --> define os caracteres que devem ser lidos
se _ antes de _%d
"_%[^\n]" --> lê uma sequeência até encontra o \n (não lê o \n)
%d - %f - %s --> já pulam espaços brancos antes dos números
" %" --> espaço em branco antes do %, pula espaços em branco


### Casting em C
- 
  
