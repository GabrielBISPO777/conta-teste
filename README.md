
usuarios = []
contas = []
transacoes = {}

def cadastrar_usuario(nome, cpf):
    for usuario in usuarios:
        if usuario["cpf"] == cpf:
            print("Usuário já cadastrado.")
            return
    usuarios.append({"nome": nome, "cpf": cpf})
    print("Usuário cadastrado com sucesso.")

def cadastrar_conta(cpf):
    for usuario in usuarios:
        if usuario["cpf"] == cpf:
            numero_conta = len(contas) + 1
            contas.append({"numero": numero_conta, "cpf": cpf, "saldo": 0})
            transacoes[numero_conta] = []
            print(f"Conta {numero_conta} cadastrada com sucesso.")
            return
    print("CPF não encontrado. Cadastre o usuário primeiro.")

def depositar(numero_conta, valor):
    for conta in contas:
        if conta["numero"] == numero_conta:
            conta["saldo"] += valor
            transacoes[numero_conta].append(f"Depósito: +R${valor:.2f}")
            print("Depósito realizado com sucesso.")
            return
    print("Conta não encontrada.")

def sacar(numero_conta, valor):
    for conta in contas:
        if conta["numero"] == numero_conta:
            if conta["saldo"] >= valor:
                conta["saldo"] -= valor
                transacoes[numero_conta].append(f"Saque: -R${valor:.2f}")
                print("Saque realizado com sucesso.")
            else:
                print("Saldo insuficiente.")
            return
    print("Conta não encontrada.")

def exibir_extrato(numero_conta):
    for conta in contas:
        if conta["numero"] == numero_conta:
            print(f"Extrato da conta {numero_conta}:")
            for t in transacoes[numero_conta]:
                print(t)
            print(f"Saldo atual: R${conta['saldo']:.2f}")
            return
    print("Conta não encontrada.")
