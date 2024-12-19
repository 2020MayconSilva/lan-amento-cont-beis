# lan-amento-cont-beis
Projeto de automação para lançamentos contábeis e cadastro de empresas, utilizando Selenium para automação web e OpenPyXL para leitura de planilhas com informações das empresas.
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
from time import sleep
import openpyxl

# Configurar o driver do navegador
driver = webdriver.Chrome(service=Service(ChromeDriverManager().install()))

# Acessar o site desejado
driver.get("https://contabilidade-devaprender.netlify.app/")  

# Aguarda o carregamento da página
sleep(3)  # Ajuste o tempo conforme necessário

# Localiza o campo de e-mail pelo seletor apropriado
email= driver.find_element(By.XPATH, "//input[@id='email']")  # Substitua ID pelo método adequado (ex: NAME, CLASS_NAME)

# Digita o e-mail no campo localizado
email.send_keys("exemplo@gmail.com")

# Localiza o campo de senha
senha = driver.find_element(By.XPATH, "//input[@id='senha']")  # Substitua ID pelo método adequado (ex: NAME, CLASS_NAME)

# Digita a senha no campo localizado
senha.send_keys("12345678")

button_entra = driver.find_element(By.XPATH, "//button[@id='Entrar']")  
button_entra.click()

# acesso completo 
sleep(3)
empresas = openpyxl.load_workbook('./empresas.xlsx')
pagina = empresas ['dados empresas']

for linha in pagina.iter_rows(min_row=2, values_only=True): 
    (nome_empresa, email, telefone, endereco, cnpj, 
     area_atuacao, quantidade_de_funcionarios, data_fundacao) = linha
    
    driver.find_element(By.ID, 'nomeEmpresa').send_keys(nome_empresa)
    sleep(1)
    driver.find_element(By.ID, 'emailEmpresa').send_keys(email)
    sleep(1)
    driver.find_element(By.ID, 'telefoneEmpresa').send_keys(telefone)
    sleep(1)
    driver.find_element(By.ID, 'enderecoEmpresa').send_keys(endereco)
    sleep(1)
    driver.find_element(By.ID, 'cnpj').send_keys(cnpj)
    sleep(1)
    driver.find_element(By.ID, 'areaAtuacao').send_keys(area_atuacao)
    sleep(1)
    driver.find_element(By.ID, 'numeroFuncionarios').send_keys(quantidade_de_funcionarios)
    sleep(1)
    driver.find_element(By.ID, 'dataFundacao').send_keys(data_fundacao)
    sleep(1)
    
    driver.find_element(By.ID, 'Cadastrar').click()
    sleep(3)
