# Calculadora

#include <stdio.h>
#include <stdlib.h>
#include <ctype.h>

void exibirMenu() {
    printf("===============================\n");
    printf("       Calculadora Simples\n");
    printf("===============================\n");
    printf("Selecione uma operação:\n");
    printf("1. Adição\n");
    printf("2. Subtração\n");
    printf("3. Multiplicação\n");
    printf("4. Divisão\n");
    printf("5. Sair\n");
    printf("Opção: ");
}

int main() {
    int opcao;
    double num1, num2, resultado;
    char continuar;

    do {
        exibirMenu();
        if (scanf("%d", &opcao) != 1) {
            printf("Erro: Entrada inválida. Por favor, digite um número inteiro entre 1 e 5.\n");
            // Limpar o buffer de entrada
            while (getchar() != '\n');
            continue;
        }
        // Limpar o buffer após ler a opção (importante para evitar problemas com o próximo scanf)
        while (getchar() != '\n');

        if (opcao < 1 || opcao > 5) {
            printf("Erro: Opção inválida. Por favor, digite um número entre 1 e 5.\n");
            continue;
        }

        if (opcao == 5) {
            printf("Obrigado por usar a calculadora! Até a próxima.\n");
            break;
        }

        printf("Digite o primeiro número: ");
        if (scanf("%lf", &num1) != 1) {
            printf("Erro: Entrada inválida. Por favor, digite um número.\n");
            while (getchar() != '\n');
            continue;
        }
        while (getchar() != '\n'); // Limpar o buffer

        printf("Digite o segundo número: ");
        if (scanf("%lf", &num2) != 1) {
            printf("Erro: Entrada inválida. Por favor, digite um número.\n");
            while (getchar() != '\n');
            continue;
        }
        while (getchar() != '\n'); // Limpar o buffer

        switch (opcao) {
            case 1:
                resultado = num1 + num2;
                printf("Resultado: %.2f + %.2f = %.2f\n", num1, num2, resultado);
                break;
            case 2:
                resultado = num1 - num2;
                printf("Resultado: %.2f - %.2f = %.2f\n", num1, num2, resultado);
                break;
            case 3:
                resultado = num1 * num2;
                printf("Resultado: %.2f * %.2f = %.2f\n", num1, num2, resultado);
                break;
            case 4:
                if (num2 == 0) {
                    printf("Erro: Divisão por zero não é permitida.\n");
                } else {
                    resultado = num1 / num2;
                    printf("Resultado: %.2f / %.2f = %.2f\n", num1, num2, resultado);
                }
                break;
            default:
                break;
        }

        if (opcao >= 1 && opcao <= 4) {
            printf("Deseja realizar outra operação? (s/n): ");
            if (scanf("%c", &continuar) != 1) {
                printf("Erro na leitura da resposta.\n");
                while (getchar() != '\n');
                break;
            }
            continuar = tolower(continuar);
            while (continuar != 's' && continuar != 'n') {
                printf("Resposta inválida. Por favor, digite 's' para sim ou 'n' para não: ");
                while (getchar() != '\n');
                if (scanf("%c", &continuar) != 1) {
                    printf("Erro na leitura da resposta.\n");
                    exit(EXIT_FAILURE);
                }
                continuar = tolower(continuar);
            }
        } else {
            continuar = 'n';
        }

    } while (continuar == 's');

    return 0;
}

