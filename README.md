# Sistema-Bancario-com-Programa-o-Orientada-a-Objetos

Desenvolvimento do Sistema Bancário com POO

Etapa 1: Criar a Classe ContaBancaria

class ContaBancaria:
    def __init__(self, saldo_inicial=0, extrato_inicial=None):
        self._numero_conta = id(self)  # Simples identificador único
        self.saldo = saldo_inicial
        self.extrato = extrato_inicial if extrato_inicial else []

        Etapa 2: Métodos de Operações Bancárias

        from datetime import datetime

    def consultar_saldo(self):
        print(f"Saldo atual: R$ {self.saldo:.2f}")

    def depositar(self, valor):
        if valor > 0:
            self.saldo += valor
            self.extrato.append({
                "data": datetime.now().isoformat(),
                "tipo": "Depósito",
                "valor": valor
            })
            print("Depósito realizado com sucesso.")
        else:
            print("Valor inválido para depósito.")

    def sacar(self, valor):
        if valor > 0 and valor <= self.saldo:
            self.saldo -= valor
            self.extrato.append({
                "data": datetime.now().isoformat(),
                "tipo": "Saque",
                "valor": valor
            })
            print("Saque realizado com sucesso.")
        else:
            print("Saldo insuficiente ou valor inválido.")

            Etapa 3: Extrato e Transferência

             def exibir_extrato(self):
        print("Extrato da conta:")
        for transacao in self.extrato:
            print(f"{transacao['data']} - {transacao['tipo']}: R$ {transacao['valor']:.2f}")

    def transferir(self, conta_destino, valor):
        if valor > 0 and valor <= self.saldo:
            self.saldo -= valor
            conta_destino.depositar(valor)
            self.extrato.append({
                "data": datetime.now().isoformat(),
                "tipo": "Transferência enviada",
                "valor": valor
            })
            print("Transferência realizada com sucesso.")
        else:
            print("Saldo insuficiente ou valor inválido.")

        Etapa 4: Persistência com JSON

        import json

def salvar_dados(conta, filename="banco_dados.json"):
    dados = {
        "saldo": conta.saldo,
        "extrato": conta.extrato
    }
    with open(filename, "w") as f:
        json.dump(dados, f)

def carregar_dados(filename="banco_dados.json"):
    try:
        with open(filename, "r") as f:
            dados = json.load(f)
            return ContaBancaria(dados["saldo"], dados["extrato"])
    except FileNotFoundError:
        return ContaBancaria()

      Etapa 5: Loop Principal

      def menu():
    print("\n1 - Consultar saldo")
    print("2 - Depositar")
    print("3 - Sacar")
    print("4 - Exibir extrato")
    print("5 - Sair")

minha_conta = carregar_dados()

while True:
    menu()
    try:
        opcao = int(input("Escolha uma opção: "))
        if opcao == 1:
            minha_conta.consultar_saldo()
        elif opcao == 2:
            valor = float(input("Valor do depósito: "))
            minha_conta.depositar(valor)
        elif opcao == 3:
            valor = float(input("Valor do saque: "))
            minha_conta.sacar(valor)
        elif opcao == 4:
            minha_conta.exibir_extrato()
        elif opcao == 5:
            salvar_dados(minha_conta)
            print("Saindo... Dados salvos.")
            break
        else:
            print("Opção inválida.")
    except ValueError:
        print("Entrada inválida. Digite um número.")
        
            
