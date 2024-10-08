
# Gerador de script MPLS VSI entre 2 equipamentos

Este repositório contém dois scripts em Python que automatizam a geração de scripts de configuração MPLS para redes de telecomunicações. Ambos os scripts são projetados para facilitar a criação de configurações para dois lados de uma conexão (LADO A e LADO B), permitindo a entrada de parâmetros como VLAN, nome, e endereços IP dos peers.

## Scripts

### 1. `mpls_range_vsi.py`

Este script gera configurações MPLS para um intervalo de VLANs especificado. Ele cria dois arquivos de script, um para o LADO A e outro para o LADO B.

#### Funcionalidades:
- **Validação de VLAN:** Verifica se a VLAN é um número válido.
- **Validação de Nome:** Assegura que o nome inserido não contém espaços.
- **Validação de Peer:** Verifica se os endereços IP dos peers são válidos no formato IPv4.
- **Geração de Scripts:** Cria configurações para cada VLAN dentro do intervalo especificado e as salva em arquivos de texto separados para o LADO A e LADO B.

#### Como usar:
1. Execute o script.
2. Insira a VLAN inicial e final, nome, e os endereços IP dos peers quando solicitado.
3. O script gerará dois arquivos `.txt` com as configurações para o LADO A e LADO B.

### 2. `mpls_vsi.py`

Este script gera uma configuração MPLS para uma única VLAN, criando um script que contém as configurações tanto para o LADO A quanto para o LADO B em um único arquivo.

#### Funcionalidades:
- **Validação de VLAN:** Verifica se a VLAN é um número válido.
- **Validação de Nome:** Assegura que o nome inserido não contém espaços.
- **Validação de Peer:** Verifica se os endereços IP dos peers são válidos no formato IPv4.
- **Geração de Scripts:** Cria configurações para a VLAN especificada, incluindo ambas as partes em um único arquivo.

#### Como usar:
1. Execute o script.
2. Insira a VLAN, nome, e os endereços IP dos peers quando solicitado.
3. O script gerará um arquivo `.txt` com as configurações para ambos os lados.

## Exemplo de Uso

### Execução do Script com Intervalo de VLANs
```bash
python mpls_range_vsi.py
```
#### Resultado no .txt do LADO A

```bash
#
vlan 2
 description MPLS_TESTE
#
vsi vlan2 static
 pwsignal ldp
  vsi-id 2
  peer 10.0.0.1
#
interface Vlanif2
 description MPLS_TESTE
 l2 binding vsi vlan2
#

#
vlan 3
 description MPLS_TESTE
#
vsi vlan3 static
 pwsignal ldp
  vsi-id 3
  peer 10.0.0.1
#
interface Vlanif3
 description MPLS_TESTE
 l2 binding vsi vlan3
#
```
#### Resultado no .txt do LADO B

```bash
#
vlan 2
 description MPLS_TESTE
#
vsi vlan2 static
 pwsignal ldp
  vsi-id 2
  peer 10.0.0.2
#
interface Vlanif2
 description MPLS_TESTE
 l2 binding vsi vlan2
#

#
vlan 3
 description MPLS_TESTE
#
vsi vlan3 static
 pwsignal ldp
  vsi-id 3
  peer 10.0.0.2
#
interface Vlanif3
 description MPLS_TESTE
 l2 binding vsi vlan3
#
```

### Execução do Script para uma VLAN
```bash
python mpls_vsi.py
```

#### Resultado no .txt

#### LADO A ####

```bash
#
vlan 3
 description MPLS_10.10.10.1
#
vsi vlan3 static
 pwsignal ldp
  vsi-id 3
  peer 10.10.10.1
#
interface Vlanif3
 description MPLS_10.10.10.1
 l2 binding vsi vlan3
#
#### LADO B ####
#
vlan 3
 description MPLS_10.10.10.1
#
vsi vlan3 static
 pwsignal ldp
  vsi-id 3
  peer 10.10.10.1
#
interface Vlanif3
 description MPLS_10.10.10.1
 l2 binding vsi vlan3
#
```

## Requisitos

- Python 3.x
- Não é necessário instalar bibliotecas adicionais.

## Licença

Este projeto está licenciado sob a Licença MIT - veja o arquivo [LICENSE](LICENSE) para mais detalhes.
