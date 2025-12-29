# Automação de Processamento de Dados (Lista para Excel) 📊

Este repositório contém um script Python desenvolvido para automatizar uma tarefa recorrente no meu fluxo de trabalho profissional: a conversão e padronização de listas textuais brutas para o formato Microsoft Excel (.xlsx).

Passo 1 (Motivação): No dia a dia de trabalho, frequentemente recebemos grandes volumes de dados em formato de texto simples ou listas desorganizadas. Este script foi criado para garantir agilidade total no processamento de centenas de itens em segundos, padronização na limpeza automática de espaços extras e integridade absoluta na redução de erros humanos comuns em preenchimentos manuais.

Passo 2 (Tecnologias Utilizadas): O projeto foi desenvolvido utilizando a linguagem Python 3.x, utilizando a biblioteca Pandas como ferramenta principal para a manipulação de dados e o motor OpenPyXL para garantir compatibilidade total com o formato Excel moderno.

Passo 3 (Como Executar o Projeto): Primeiro, você deve clonar este repositório para sua máquina local. Segundo, instale as dependências necessárias executando o comando "pip install pandas openpyxl" em seu terminal. Terceiro, insira sua lista de dados brutos na variável definida dentro do arquivo "processor.py" e execute o script para gerar o arquivo final formatado.

Passo 4 (Boas Práticas Aplicadas): O código foi estruturado seguindo as diretrizes da PEP 8, utilizando modularização através de funções reutilizáveis, Type Hinting para facilitar a leitura técnica, tratamento de erros (try/except) para evitar falhas de sistema e sanitização automática de dados com o método .strip() para garantir dados limpos.

---
# Código em Python

import pandas as pd
import os
from typing import List

def exportar_lista_para_excel(dados: List[str], nome_arquivo: str, nome_coluna: str = "Respostas") -> None:
    """
    Converte uma lista de strings em uma planilha Excel formatada.
    
    Esta função automatiza a criação de DataFrames, realiza a limpeza básica 
    dos dados (remoção de espaços) e exporta o resultado final.
    """
    try:
        # 1. Validação inicial: verifica se há dados para processar
        if not dados:
            print("⚠️ Aviso: A lista de dados está vazia. Nada foi processado.")
            return

        print(f"🔄 Iniciando processamento de {len(dados)} itens...")
        
        # 2. Criação do DataFrame (Tabela) utilizando a biblioteca Pandas
        df = pd.DataFrame(dados, columns=[nome_coluna])
        
        # 3. Data Cleaning: Remove espaços em branco extras no início e fim de cada texto
        df[nome_coluna] = df[nome_coluna].astype(str).str.strip()
        
        # 4. Exportação para Excel (.xlsx) utilizando o motor openpyxl
        # index=False evita que o Excel crie uma coluna de números (índices) desnecessária
        df.to_excel(nome_arquivo, index=False, engine='openpyxl')
        
        print(f"✅ Sucesso! O arquivo '{nome_arquivo}' foi gerado no diretório atual.")
        
    except Exception as e:
        # Tratamento de erro para capturar falhas de permissão ou falta de bibliotecas
        print(f"❌ Ocorreu um erro inesperado: {e}")

if __name__ == "__main__":
    # --- ÁREA DE CONFIGURAÇÃO DO USUÁRIO ---
    # Substitua os itens desta lista pelos dados que você deseja processar
    minha_lista_de_trabalho = [
        "Itaú", 
        "Simeticona", 
        "Coca-Cola", 
        "Vivo", 
        "Heineken", 
        "Luftal",
        "Riachuelo",
        "Santander"
    ]
    
    # Nome do arquivo que será criado
    arquivo_saida = "Relatorio_Processado.xlsx"
    
    # Execução da automação
    exportar_lista_para_excel(
        dados=minha_lista_de_trabalho, 
        nome_arquivo=arquivo_saida,
        nome_coluna="Itens_Identificados"
    )
    ---
Desenvolvido por [Murilo Cunha] – [(https://www.linkedin.com/in/murilo-cunha-71aa72299/]

