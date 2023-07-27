menu = """

======== Menu ========

[1] Depositar
[2] Sacar
[3] Extrato
[0] Sair

======================

=> """

saldo = 0
LIMITE_SAQUES_DIARIOS = 3
limite_de_saque = 1000
extrato = ""
numero_saques = 0

while True:

    opcao = input(menu)

    if opcao == "1":
        valor = float(input("Digite o valor de deposito: "))

        if valor > 0:
            saldo += valor
            extrato += f"Depósito: R$ {valor:.2f}\n"
            print(f"Deposito de", valor, "reais realizado com sucesso. ")
            
        else:
            print("Operação falhou! o valor informado é invalido")

    elif opcao == "2":
        valor = float(input("Digite o valor de saque: "))

        excedeu_saldo = valor > saldo

        excedeu_limite = valor > limite_de_saque

        excedeu_saques = numero_saques >= LIMITE_SAQUES_DIARIOS

        #A variavel para_da_certo vai receber true se o que esta entre parenteses for true e recebe false caso o que esta entre parenteses for false
        para_dar_certo = (saldo >= valor)
               
        if excedeu_limite:
            print("Operação falhou! O valor do saque excede o limite")

        elif excedeu_saques:
            print("Operação falhou! Número máximo de saques excedido.")

        elif valor > 0 and saldo >= valor:
            saldo -= valor
            extrato += f'Saque: R$ {valor:.2f}\n'
            numero_saques += 1

            if para_dar_certo:
                    print("Operação sucessida! Você sacou", valor, "reais com sucesso. ")

        elif excedeu_saldo:
            print("Operação falhou! Você não tem saldo suficiente")
                           
        else:
            print("Operação falhou! O valor informado é invalido.")
              
    elif opcao == "3":
        print("\n============== EXTRATO ==============")
        print("Não foram realizados movimentações." if not extrato else extrato)
        print(f'\nSaldo: R$ {saldo:.2f}')
        print("=====================================")
    
    elif opcao == "0":
        break 

    else:
        print("Operacao Inválida, por favor selecione novamente a operação desejada.")
