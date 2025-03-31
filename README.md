# Calculadora

#include <stdio.h>
#include <stdlib.h>
#include <ctype.h>

// Função para exibir o menu
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

        printf("Digite o segundo número: ");
        if (scanf("%lf", &num2) != 1) {
            printf("Erro: Entrada inválida. Por favor, digite um número.\n");
            while (getchar() != '\n');
            continue;
        }

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
                // Já tratado acima, mas para evitar warnings
                break;
        }

        if (opcao >= 1 && opcao <= 4) {
            printf("Deseja realizar outra operação? (s/n): ");
            // Limpar o buffer de entrada de qualquer caractere newline pendente
            while (getchar() != '\n');
            if (scanf("%c", &continuar) != 1) {
                printf("Erro na leitura da resposta.\n");
                break;
            }
            continuar = tolower(continuar);
            while (continuar != 's' && continuar != 'n') {
                printf("Resposta inválida. Por favor, digite 's' para sim ou 'n' para não: ");
                while (getchar() != '\n');
                if (scanf("%c", &continuar) != 1) {
                    printf("Erro na leitura da resposta.\n");
                    exit(EXIT_FAILURE); // Encerra o programa em caso de erro grave
                }
                continuar = tolower(continuar);
            }
        } else {
            continuar = 'n'; // Para sair do loop após a opção 5
        }

    } while (continuar == 's');

    return 0;
}
