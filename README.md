login = []
pacientes = [
    ['12345678900', 'Maria Silva', '1234', '88999999999', 'Alergia a dipirona'],
    ['98765432100', 'Joao Santos', '5678', '88988888888', 'Nenhuma alergia'],
    ['45678912300', 'Ana Oliveira', '4321', '88977777777', 'Alergia a anestesia'],
    ['32165498700', 'Pedro Costa', '8765', '88966666666', 'Nenhuma observacao']
]
odonto_dados = [['Dra. Lucia','Ortondotia', '25266','13'],
                ['Dra. Ana','Facetas','22332','30'],
                ['Dr. Gustavo','Implantodontia','16112', '24']
]
odonto_user = []
odonto_vinculo = []
hor_atend = ['08:00', '09:00', '10:00', '11:00']
consultas = [
    ['12345678900', 'Dra. Lucia', '05/11/2026', '08:00'],
    ['98765432100', 'Dra. Ana', '05/11/2026', '09:00'],
    ['45678912300', 'Dr. Gustavo', '06/11/2026', '10:00'],
    ['32165498700', 'Dra. Lucia', '06/11/2026', '11:00']
]
salas = []
while True:
    print('\n--- MENU PRINCIPAL ---')
    print('1. AREA PACIENTE')
    print('2. AREA ADMINISTRAÇÃO')
    print('0. SAIR')

    opcao = input('Escolha uma opcao: ')
    
    if opcao == '0':
        break

    elif opcao == '1':
        cpf_l = input('Informe seu CPF: ')
        senha_l = input('Digite sua senha: ')

        autologin = False
        cpf_encontrado = False

        for i in range(len(login)):
            if cpf_l == login[i][0]:
                cpf_encontrado = True

                if senha_l == login[i][1]:
                    autologin = True
                break

        if autologin:
            print('Login realizado com sucesso!')

        elif cpf_encontrado:
            print('Senha incorreta! Tente novamente.')

        else:
            print('\nCPF não encontrado! Realize seu cadastro:')

            cpf_l = input('Digite seu CPF: ')
            nome = input('Nome completo: ')
            senha = input('Crie uma senha: ')
            tel = input('Telefone para contato: ')

            login.append([cpf_l, senha, nome, tel])

            print('Cadastro realizado com sucesso!')
        while True:
            print('--- MENU PACIENTE ---')
            print('1. Ver Corpo Clinico')
            print('2. Agendar Consulta')
            print('3. Minhas Consultas')
            print('4. Cancelar Consulta') 
            print('0. Voltar Menu Principal')
            opcao_paciente = int(input('Digite a opçao desejada:')) 
            if opcao_paciente == 0:
                break

            elif opcao_paciente == 1:
                for i in range(len(odonto_dados)):
                    print('\n--- CORPO CLINICO ---')
                    print('Nome: ',odonto_dados[i][0]) 
                    print('Especialidade: ',odonto_dados[i][1])
                    print('CRO: ',odonto_dados[i][2])

            elif opcao_paciente == 2:
                print('\n--- AGENDE SUA CONSULTA ---')

                for i in range(len(odonto_dados)):
                    print(f'\nProfissionais da instituição: {odonto_dados[i][0]}, {odonto_dados[i][1]}')

                dentista = input('\nDigite o nome do profissional que irá lhe atender: ')
                dia = input('Digite a data desejada DD/MM/AAAA: ')

                horarios_livres = []

                for horario in hor_atend:
                    indisponivel = False

                    for consulta in consultas:
                        if consulta[1] == dentista and consulta[2] == dia and consulta[3] == horario:
                            indisponivel = True

                    if indisponivel == False:
                        horarios_livres.append(horario)

                print('\nHorários disponíveis:')

                for horario in horarios_livres:
                    print(horario)

                if len(horarios_livres) == 0:
                    print('Não há horários disponíveis para esse dentista nesse dia.')

                else:
                    horario = input('\nEscolha um horário: ')

                    if horario in horarios_livres:
                        consultas.append([cpf_l, dentista, dia, horario])

                        print('\n--- CONSULTA AGENDADA COM SUCESSO ---')
                        print('Dentista:', dentista)
                        print('Dia:', dia)
                        print('Horário:', horario)

                    else:
                        print('\nHorário inválido ou indisponível!')

            elif opcao_paciente == 3:
                encontrar = False
                print('\n--- MINHAS CONSULTAS ---')

                for consulta in consultas:
                    if consulta[0] == cpf_l:
                        print('\nDentista:', consulta[1])
                        print('Dia:', consulta[2])
                        print('Horário:', consulta[3])
                        encontrar = True

                if encontrar == False:
                    print('\nVocê não possui consultas.')
                            
            elif opcao_paciente == 4:
                print('\n--- CANCELAR CONSULTA ---')
                encontrar = False
                for consulta in consultas:
                    if consulta[0] == cpf_l:
                        print('\nDentista:', consulta[1])
                        print('Dia:', consulta[2])
                        print('Horario:', consulta[3])
                        encontrar = True

                if encontrar == False:
                    print('\nVoce nao possui consultas para cancelar.')
                        
                else:
                    dentista = input('\nDigite o dentista da consulta que deseja cancelar: ')
                    dia= input('Digite o dia da consulta: ')
                    horario = input('Digite o horario da consulta: ')
                    ind = -1
                    for i in range(len(consultas)):
                        if consultas[i][0] == cpf_l and consultas[i][1] == dentista and consultas[i][2] == dia and consultas[i][3] == horario:
                            ind = i
                            break
                    if ind == -1:
                                print('\nConsulta nao encontrada.')
                    else:
                        consultas.pop(ind)
                        print('\nConsulta cancelada com sucesso!')
            else:
                print('Opção invalida tente novamente')

    elif opcao == '2':
        login = input('Digite o login: ')
        senha_adm = input('Digite sua senha: ')
        if login != 'adm' or senha_adm != '123':
            print('Login ou senha incorreto')
            continue
        while True:
            print(
                '\n----MENU----\n1- Gestão de Dentistas \n2- Gestão de Consultórios\n3- Gestão de Pacientes\n4- Gestão de Agenda Geral\n5- Sair\n')
            op_gestao = int(input('Qual a opção desejada? '))
            if op_gestao == 1:
                while True:
                    print('\n----MENU----' \
                    '\n1- Cadastrar ' \
                    '\n2- Listar ' \
                    '\n3- Buscar ' \
                    '\n4- Atualizar ' \
                    '\n5- Remover dentistas'
                    '\n0- Sair')   
                    op_adm = int(input('Digite a opção desejada: '))
                    if opcao == 0:
                        break
                    elif op_adm == 1:
                        n_adm = input('Digite o nome: ')
                        cro = int(input('Digite seu CRO: '))
                        esp = input('Digite sua especialidade: ')
                        id = int(input('Digite o ID: '))
                        odonto_dados.append(n_adm)
                        odonto_dados.append(cro)
                        odonto_dados.append(esp)
                        odonto_dados.append(id)
                        print('Especialista cadastrado com sucesso!')

                    elif op_adm == 2:
                        for i in range(len(odonto_dados)):
                            print('\nNome: ',odonto_dados[i][0]) 
                            print('Especialidade: ',odonto_dados[i][2])
                            print('CRO: ',odonto_dados[i][1])
                            
                    elif op_adm == 3:
                        buscar = input('\nQual especialista deseja buscar? ')
                        for buscar in odonto_dados:
                            print(buscar, ', era o especialista que buscava. ')
                            break
                    
                    elif op_adm == 4:
                        atualizar_D = input('Informe o ID do paciente para atualizacoes: ')  
                        encontrar = False
                        for odonto_dado in odonto_dados:
                            if odonto_dado[3] == atualizar_D:
                                encontrado = True 

                        print('\n1- Nome \n2- CRO \n3- Especialidade')
                        atu = input('Qual dado deseja atualizar? ')
                        if atu == '1':
                            odonto_dados.pop(0)
                            nome = input('Digite o novo nome: ')
                            odonto_dados.insert(0, nome)
                            print('Dados atualizados com sucesso!')
                        elif atu == '2':
                            odonto_dados.pop(1)
                            cron = input('Digite seu novo CRO: ')
                            odonto_dados.insert(1, cron)
                            print('Dados atualizados com sucesso!')
                        elif atu == '3':
                            odonto_dados.pop(2)
                            esp = input('Digite a nova especialidade: ')
                            odonto_dados.insert(2, esp)
                            print('Dados atualizados com sucesso!')

                        else:
                            print('Opção inválida!')

                    elif op_adm == 5:
                        remover = input('\nQual o nome do dentista deseja remover? ')
                        ind = -1
                        for i in range(len(odonto_dados)):
                            if remover == odonto_dados[i]:
                                ind = i
                        if ind != -1:
                            odonto_dados.pop(ind)
                            odonto_dados.pop(ind)
                            odonto_dados.pop(ind)
                            odonto_dados.pop(ind)
                            print('Dentista removido com sucesso!')
                        else:
                            print('Dentista não encontrado!')
                            
            elif op_gestao == 2:
                print('\n----MENU----' \
                '\n1- Cadastrar ' \
                '\n2- Vincular ' \
                '\n3- Listar salas e dentistas' \
                '\n0- Sair')
                op_cons = int(input('Qual a opção desejada? '))
                
                if opcao == '0':
                    break
                elif op_cons == 1:
                    ns = int(input('\nDigite o número da sala: '))
                    salas.append(ns)
                    print('Sala cadastrada com sucesso!')
            
                elif op_cons == 2:
                    print(odonto_dados)
                    destista_vincular = input('Esses são os dentistas disponiveis, escolha qual quer vincular: ')
                    print(salas)
                    vincularsala = int(input('Digite qual sala quer vincular ao dentista: '))
                    odonto_vinculo.append(destista_vincular)
                    odonto_vinculo.append(vincularsala)
                    print('Sala e dentista vinculada com sucesso!')
                
                elif op_cons == 3:
                    print(odonto_vinculo)

            elif op_gestao == 3:
                while True:
                    print('\n--- MENU PACIENTE ---')
                    print('1. Cadastrar de pacientes')
                    print('2. Listar/Buscar por pacientes')
                    print('3. Atualizar dados cadastrais e Adicionar observações/Alergias') 
                    print('0. Voltar Menu Principal')
                    op_gest_pacie = int(input('Qual a opcao desejada? '))
                    if op_gest_pacie == 0:
                        break
                    elif op_gest_pacie == 1:
                        cpf_p = input('CPF: ')
                        nome_p = input('Nome: ') 
                        telef_p = input('Telefone: ')
                        senha_p = input('Senha: ')
                        obs_p = input('Observarçoes/Alergias: ')

                        paciente_novo = [cpf_p, nome_p, senha_p, telef_p, obs_p]
                        pacientes.append(paciente_novo)
                        print('Paciente cadastrado com sucesso!')

                    elif op_gest_pacie == 2:
                        listar_buscar = input('\n1.Listar todos os pacientes: ' \
                        '\n2.Buscar paciente por CPF/Nome:')

                        if listar_buscar == '1':
                            for i in range(len(pacientes)):
                                print('\nCPF: ',pacientes[i][0])
                                print('Nome: ',pacientes[i][1])
                                print('Telefone: ',pacientes[i][3])
                                print('Alergia/Observacao: ',pacientes[i][4])
                            
                        elif listar_buscar == '2':
                            buscarcpf_nome = input('\nInforme CPF ou o nome: ')
                            achado = False

                            for i in range(len(pacientes)):
                                if buscarcpf_nome in pacientes[i][0] or buscarcpf_nome in pacientes[i][1]:
                                    print('\nPaciente encontrado!')
                                    print('Nome:', pacientes[i][1])
                                    print('CPF:', pacientes[i][0])
                                    print('Telefone:', pacientes[i][3])
                                    print('Observaçoes e alergias',pacientes[i][4])
                                    achado = True

                            if achado == False:
                                print('\nPaciente nao encontrado. ')
                        else:
                            print('Nao ha pacientes cadastrados')

                    elif op_gest_pacie == 3:
                        atualizar_p = input('Informe o CPF do paciente para atualizacoes: ')  
                        encontrar = False
                        for paciente in pacientes:
                            if paciente[0] == atualizar_p:
                                encontrado = True 

                        print('1.Atualizar o Nome: ')
                        print('2.Atualizar o Senha: ')
                        print('3.Atualizar o Telefone: ')
                        print('4.Adicionar Obersevaçao ou Alergia: ')
                                
                        op_alterar = int(input('Escolha o de deseja atualizar: '))
                                    
                        if op_alterar == 1:
                            novo_nome = input('Digite o novo nome: ')
                            paciente[1] = novo_nome
                            print('Nome atualizado com sucesso!')
    
                        elif op_alterar == 2:
                            novo_senha = input('Informe a nova senha: ')
                            paciente[2] = novo_senha
                            print('Senha atualizado com sucesso!')
    
                        elif op_alterar == 3:
                            novo_fone = input('Informe o novo numero de contato: ')
                            pacientes[3] = novo_fone
                            print('Telefone atualizado com sucesso!')
    
                        elif op_alterar == 4:
                            novo_obs = input('Adicione ou modifique alergias e observacoes ao pacinte: ')
                            pacientes[4] = novo_obs
                            print('Adicionado com sucesso!')
                        
                        else: 
                            print('Opcao invalida!')
                            break
                    elif encontrar == False:
                        print('Paciente nao encontrado!')
                    else:
                        print('Opcao invalida!')               
            
            elif op_gestao == 4:

                while True:
                    print('\n--- GESTÃO DE AGENDA GERAL ---')
                    print('1. Visualizar agenda completa da clínica')
                    print('2. Filtrar agendamentos')
                    print('3. Cancelar consulta de qualquer paciente')
                    print('0. Voltar ao menu administrativo')

                    op_agenda = input('\nEscolha uma opção: ')

                    if op_agenda == '1':
                        print('\n--- AGENDA COMPLETA DA CLÍNICA ---')
                        if len(consultas) == 0:
                            print('Não existem consultas agendadas.')
                        else:
                            for i in range(len(consultas)):
                                cpf = consultas[i][0]
                                nome_paciente = 'Paciente não identificado'
                                for paciente in pacientes:
                                        if paciente[0] == cpf:
                                            nome_paciente = paciente[1]
                                            break
                                print(f'\nConsulta {i + 1}')
                                print('Paciente:', nome_paciente)
                                print('CPF:', cpf)
                                print('Dentista:', consultas[i][1])
                                print('Data:', consultas[i][2])
                                print('Horário:', consultas[i][3])

                    elif op_agenda == '2':

                        print('\n--- FILTRAR AGENDAMENTOS ---')
                        print('1. Filtrar por dentista')
                        print('2. Filtrar por data')
                        filtro = input('Escolha uma opção: ')
                        encontrou = False
                        if filtro == '1':
                            dentista_filtro = input('\nDigite o nome do dentista: ')
                            for consulta in consultas:
                                if consulta[1].lower() == dentista_filtro.lower():
                                    cpf = consulta[0]
                                    nome_paciente = 'Paciente não identificado'

                                    for paciente in pacientes:
                                        if paciente[0] == cpf:
                                            nome_paciente = paciente[1]
                                            break

                                    print('\n--- AGENDAMENTO ENCONTRADO ---')
                                    print('Paciente:', nome_paciente)
                                    print('CPF:', cpf)
                                    print('Dentista:', consulta[1])
                                    print('Data:', consulta[2])
                                    print('Horário:', consulta[3])
                                    encontrou = True
                        elif filtro == '2':
                            data_filtro = input('\nDigite a data desejada (DD/MM/AAAA): ')
                            for consulta in consultas:
                                if consulta[2] == data_filtro:
                                    cpf = consulta[0]
                                    nome_paciente = 'Paciente não identificado'
                                    for paciente in pacientes:
                                            if paciente[0] == cpf:
                                                nome_paciente = paciente[1]
                                                break
                                    print('\n--- AGENDAMENTO ENCONTRADO ---')
                                    print('Paciente:', nome_paciente)
                                    print('CPF:', cpf)
                                    print('Dentista:', consulta[1])
                                    print('Data:', consulta[2])
                                    print('Horário:', consulta[3])
                                    encontrou = True
                        else:
                            print('Opção inválida!')

                        if not encontrou:
                            print('\nNenhum agendamento encontrado.')

                    elif op_agenda == '3':
                        print('\n--- CANCELAR CONSULTA ---')
                        if len(consultas) == 0:
                            print('Não existem consultas para cancelar.')
                        else:
                            print('\nConsultas cadastradas:')
                            for i in range(len(consultas)):
                                cpf = consultas[i][0]
                                nome_paciente = 'Paciente não identificado'

                                for paciente in pacientes:
                                    if paciente[0] == cpf:
                                        nome_paciente = paciente[1]
                                        break

                                print(f'\nConsulta {i + 1}')
                                print('Paciente:', nome_paciente)
                                print('CPF:', cpf)
                                print('Dentista:', consultas[i][1])
                                print('Data:', consultas[i][2])
                                print('Horário:', consultas[i][3])

                            numero = int(input('\nDigite o número da consulta que deseja cancelar: '))

                            if numero >= 1 and numero <= len(consultas):
                                consulta_cancelada = consultas.pop(numero - 1)
                                print('\nConsulta cancelada com sucesso!')
                                print('CPF do paciente:', consulta_cancelada[0])
                                print('Dentista:', consulta_cancelada[1])
                                print('Data:', consulta_cancelada[2])
                                print('Horário:', consulta_cancelada[3])
                            else:
                                print('\nNúmero de consulta inválido!')
                    elif op_agenda == '0':
                        break
                    else:
                        print('\nOpção inválida! Tente novamente.')
            elif op_gestao == 5:
                break
    else:
        print('Opcao invalida')
