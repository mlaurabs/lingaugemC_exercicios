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
  - biblioteca: <stdib.h>
  - tratamento de erro: exit()
    - aborta o programa
  - função malloc()
    - reserva em memória uma array de bytes
    - retorna um ponteiro genérico --> void*
    - retorna NULL, caso haja algum erro. Ex.: não há memória sufuciente no sistema
- função free()
    - recebe como parâmetro um ponteiro que aponta para uma memória alocada
    - a função free() libera o espaço em memória
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

- Abrir arquivo:
  - ***FILE* f = fopen("path", "rt / wt / rb / wb")***

- Fechar arquivos:
    - **flcose(ponteiro do arquivo)**

- Arquivos text:
  - leitura --> "rt"
  - escrita --> "wt"
  - Métodos de leitura:
    - **fscanf(ponteiro do arquivo, formato de leitura, endereço da variável(s) ou variaveis que vão receber o conteúdo lido)**
      - este método retorna o número de parâmetros lidos
      - getc() e fgetc() lidam com a leitura de caracteres (Ex.: char c = getc(ponteiro do arquivo))
  - Método de escrita:
    - **fprintf(ponteiro do arquivo, formato de leitura, variável(s) ou variaveis)**

***OBS.: FEOF(ponteiro do arquivo) --> retorna True quando encontra o "end of file"/EOF***

- Arquivo binário
  - leitura --> "rb"
  - escrita --> "wb"
  - Método de escrita:
     - **fwrite(ponteiro q aponta para o que vai ser escrito, tamanho em bytes de cada item a ser escrito, número de itens a serem escritos, ponteiro do arquivo)**
       - Ex.: int x; fwrite(&x, sizeof(int), 1, f) / int vetor[3] = {10, 20, 30}; fwrite(vetor, sizeof(int), 3);
  - Método de leitura:
    - **fread(ponteiro q aponta para o que vai ser escrito, tamanho em bytes de cada item a ser escrito, número de itens a serem escritos, ponteiro do arquivo)**
      - Ex.: int y; fread(&y, sizeof(int), 1, f);
      - retorna o número de arquivos lidos
  - Deslocamento do cursor do arquivo:
      - SEEK_SET: a partir do início do arquivo
      - SEEK_CUR: a partir da posiçãao corrente do cursor
      - SEEK_END: a partir do final do arquivo (offset negativo)

### Tipos Estruturados
- é como se fosse uma "classe"
- Definindo uma estrutura:
  - struct ponto{
        float x;
        float y;
    }
```c
struct ponto{
        float x;
        float y;
}

void imprime(struct ponto p){ // desta forma, todo conteúdo de ponto (x e y) é copidado para a função
    printf("%.2f e %.2f", p.x, p.y);
}

int main(void){
    struct ponto p;

    printf("Digite as coordenadas do ponto (x y): ");
    scanf("%f %f", &p.x, &p.y);
    imprime(p);
    return 0;

}

```
- Usando alocação dinâmica:
  - Reservando espaço em memória para um tipo estruturado:
```c
struct ponto* p;
p = (struct ponto*) malloc(sizeof(struct ponto)); // alocando dinamicamente um espaço em memoria para o tipo ponto
p -> x = 12.0f; // incializando a variável do tipo ponto 
```
- **typedef** --> atribui nomes diferentes para determinados tipos
  - Ex.:
```c
typedef struct ponto{
    float x;
    float y;
}Ponto // agora o tipo "struct ponto" é referenciado como Ponto
```
### Lista Encadeada
- representada utilizando struct para representar o nó da lista

- O que é um nó?
    - o nó representa um elemento da lista encadeada
    - o nó é composto de duas partes: o dado e a referência para o próximo nó
    - quando um nó aponta para NULL, está no último nó/elemento da lista
    - O endereço de uma lista encadeada e o endereço de sua
        primeira celula. 

![Sem título](https://github.com/mlaurabs/lingaugemC_exercicios/assets/89169599/47a76b56-0024-4ed2-85bb-eef7ecdd5456)

Ex.:
```c
#define _CRT_SECURE_NO_DEPRECATE
#include <stdio.h>
#include <stdlib.h>

typedef struct nod Nod;
struct nod {
	int dado;
	Nod* prox;
};


Nod* inicia(void) {
	return NULL;
}

Nod* insere(Nod* lista, int value) { // insere no início da lista
	Nod* p = (Nod*)malloc(sizeof(Nod));
	p->dado = value;
	p->prox = lista;
	return p;
}

void imprime(Nod* lista) {
	for (Nod* p = lista; p != NULL; p = p->prox) {
		printf("\n%d", lista->dado);
	}
}

// dúvidas??
// a lista, ex.: l, sempre começa apontando pra cabeça?? é a mesma ideia de strings?
// 


void imprimeRev(Nod* lista) {
	if (lista != NULL) {
		Nod* fim = inicia();
		while (fim != lista) {
			Nod* p = lista;
			while (p->prox != fim) {
				p = p->prox;
			}
			printf("%d\n", p->dado);
			fim = p;
		}

	}
}

Nod* lremove(Nod* l, int x) {
	if(l == NULL) {
		return l;
	}else if(l->dado != x){
		l->prox = lremove(l->prox, x);
	}
	else {
		Nod* t = l->prox;
		free(l);
		return t;
	}
	return l;
}

/*
Nod* lremove(Nod* l, int x){
	    
}

*/

/*
void imprime_rev_recursao(NoLista* fazuL){
	if (fazuL == NULL){
	return;
	}
	imprime_rev_recursao(fazuL->prox);
	printf("%d\n", fazuL->info);
}
*/

Nod* insereOrd(Nod* l, int x){
	if (l == NULL || l->dado > x) {
		Nod* p = (Nod*)malloc(sizeof(Nod));
		if (p == NULL) {
			printf("Erro\n");
			exit(0);
		}
		p->dado = x;
		p->prox = l;
		return p;
	}
	else {
		l->prox = insereOrd(l->prox, x);
		return l;
	}
}

int main(void) {

	Nod* new = inicia();
	new = insere(new, 8);
	new = insere(new, 20);
	imprime(new);
	printf("\n\n");
	imprimeRev(new);
	

	return 0;
}


// Aula 10/06/2024

#define _CRT_SECURE_NO_DEPRECATE
#include <stdio.h>
#include <stdlib.h>

typedef struct nod Nod;
struct nod {
	int dado;
	Nod* prox;
};

int igual(Nod* l1, Nod* l2) {
	Nod* p1 = l1;
	Nod* p2 = l2;

	while (p1 != NULL && p2 != NULL) {
		if (p1->dado != p2->dado) {
			return 0;
		}
		p1 = p1->dado;
		p2 = p2->prox;

	}
	return p1 == p2;
}

Nod* insere(Nod* lista, int value) {
	Nod* p = (Nod*)malloc(sizeof(Nod));
	if (p == NULL) {
		// Gerenciar falha de alocação de memória aqui, como retornar a lista original
		// ou abortar o programa.
		// Exemplo de retorno da lista original:
		return lista;
	}
	p->dado = value;
	p->prox = lista;
	return p;
}


void copia(Nod* lista) {
	Nod* p = (Nod*)malloc(sizeof(Nod));
	
	Nod* ini = NULL;
	Nod* fim = NULL;

	for (Nod* p = lista; lista != NULL; p = p->prox) {
		Nod* q = (Nod*)malloc(sizeof(Nod));
		q->dado = p->dado;
		q->dado = NULL;
		if (ini == NULL) {
			ini = q;
			fim = q;
		}
		else {
			fim->prox = q;
		}
		fim = q;
	}
	return ini;
	
}

Nod* copia(Nod* lista) {
	if (lista = NULL) {
		return NULL;
	}
	else {
		Nod* p = (Nod*)malloc(sizeof(Nod));
		p->dado = lista->dado;
		p->prox = copia(lista->prox);
		return p;
	}
}

void imprime(Nod* lista) {
	for (Nod* p = lista; p != NULL; p = p->prox) {
		printf("%d\n", p->dado);
	}
}

int main(void) {

	Nod* teste = NULL;
	int v = 6;
	teste = insere(teste, v);
	teste = insere(teste, 10);
	imprime(teste);
	copia(teste);

	return  0;
}
```
