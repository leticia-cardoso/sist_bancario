# sist_bancario
Sistema bancário criado no bootcamp DIO

#Criar depósito bancário: DEPOSITO | SAQUE | EXTRATO

saldo_conta = 0
limite = 500
extrato = ""
numero_saque = 0
limite_saque = 3
extrato_deposito = []
extrato_saque = []

print("Olá, seja bem-vindo(a) à sua conta bancária!" "\n")

#depósito: apenas valores positivos, depósito armazenado numa variavel e exibido no extrato
def deposito(): 
    valor_deposito = float(input("Qual o valor deseja depositar na sua conta? "))
    if valor_deposito < 0:
        print("Erro. Digite um número válido." "\n")
    else:
        global saldo_conta 
        saldo_conta += valor_deposito
        print("Depósito realizado com sucesso!" "\n")
        extrato_deposito.append(valor_deposito)

#saque: valor menor ou igual ao saldo na conta, possível apenas 3 saques diários, com limite máximo de 500 reais por saque. 
#se não tiver dinheiro suficiente informar o erro e criar variavel armazenando os saques e exibir no extrato
def saque():
    valor_saque = float(input("Qual valor deseja sacar? "))
    global saldo_conta
    global limite_saque
    global numero_saque
    if valor_saque > saldo_conta:
        print("Saldo insuficiente." "\n")
    elif valor_saque > 500:
        print("Erro. Limite de valor excedido. " "\n")
    elif valor_saque < saldo_conta and numero_saque < limite_saque:
        saldo_conta -= valor_saque
        print("Saque feito com sucesso" "\n")
        numero_saque += 1
        extrato_saque.append(valor_saque)
    else:
        print("Erro. Limite de número de saques atingido." "\n")

#extrato: lista todos os depósitos e saques e valor atual da conta, formatado em R$00.00
def extrato():
    global extrato_deposito
    global extrato_saque
    print(f"Seu saldo atual é de: R${saldo_conta: .2f}" "\n")
        
    if extrato_deposito:
        print("Depósitos realizados: ")
        for i, extrato_deposito in enumerate(extrato_deposito, 1):
            print(f"{i}. {extrato_deposito}")
    else:
        print("Nenhum depósito realizado.")
          
    if extrato_saque:
        print("Saques realizados: ")
        for i, extrato_saque in enumerate(extrato_saque, 1):
            print(f"{i}. {extrato_saque}")
    else:
        print("Nenhum saque realizado." "\n")

#Menu com as opções
while True:
    menu = int(input('''Digite o número da opção desejada:
       1 - Depósito
       2 - Saque
       3 - Extrato
       4 - Sair
    > '''))

    if menu == 1:
        deposito()

    elif menu == 2:
        saque()

    elif menu == 3:
        extrato()

    elif menu == 4:
         print ("Operação encerrada." "\n")
         break
    else:
        print("Opção não identificada, tente novamente" "\n")
        continue
