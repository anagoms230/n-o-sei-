git clone https://github.com/ana-carolina/seu-repositorio.git
import datetime
import matplotlib.pyplot as plt

# Dicionário para armazenar as atividades e seus tempos
registro_atividades = {}

def iniciar_atividade(atividade):
    if atividade in registro_atividades:
        print("Atividade já está em andamento.")
    else:
        registro_atividades[atividade] = {'inicio': datetime.datetime.now(), 'fim': None}
        print(f"Atividade '{atividade}' iniciada.")

def finalizar_atividade(atividade):
    if atividade not in registro_atividades:
        print("Atividade não encontrada.")
    elif registro_atividades[atividade]['fim'] is not None:
        print("Atividade já foi finalizada.")
    else:
        registro_atividades[atividade]['fim'] = datetime.datetime.now()
        print(f"Atividade '{atividade}' finalizada.")

def exibir_resumo():
    print("\nResumo das atividades:")
    tempos_totais = {}
    for atividade, tempos in registro_atividades.items():
        tempo_total = tempos['fim'] - tempos['inicio'] if tempos['fim'] else datetime.timedelta(0)
        tempos_totais[atividade] = tempo_total

    # Exibir gráfico de barras com os tempos totais das atividades
    plt.figure(figsize=(10, 6))
    plt.bar(tempos_totais.keys(), [tempo.total_seconds() / 60 for tempo in tempos_totais.values()], color='skyblue')
    plt.xlabel('Atividades')
    plt.ylabel('Tempo Total (minutos)')
    plt.title('Tempo Total por Atividade')
    plt.xticks(rotation=45, ha='right')
    plt.tight_layout()
    plt.show()

def main():
    while True:
        print("\nMenu:")
        print("1. Iniciar atividade")
        print("2. Finalizar atividade")
        print("3. Exibir resumo das atividades")
        print("4. Sair do programa")
        escolha = input("Escolha uma opção: ")

        if escolha == '1':
            atividade = input("Digite o nome da atividade que deseja iniciar: ")
            iniciar_atividade(atividade)
        elif escolha == '2':
            atividade = input("Digite o nome da atividade que deseja finalizar: ")
            finalizar_atividade(atividade)
        elif escolha == '3':
            exibir_resumo()
        elif escolha == '4':
            print("Encerrando o programa.")
            break
        else:
            print("Opção inválida. Tente novamente.")

if __name__ == "__main__":
    main()
