# Web-scrapping-selenium
from selenium import webdriver
from selenium.webdriver.common.by import By
import time
lista_descricoes = []
if __name__ == '__main__':
    driver = webdriver.Chrome()
    driver.implicitly_wait(10)
    driver.maximize_window()
    driver.get('https://www.linkedin.com/jobs/ci%C3%AAncia-de-dados-vagas/?originalSubdomain=br')
    resultados = driver.find_elements(By.CLASS_NAME, 'base-card')
    while True:
        for r in resultados[len(lista_descricoes):]:
            r.click()
            time.sleep(4)
            try:
                descricao = driver.find_element(By.CLASS_NAME, 'description')
                lista_descricoes.append(descricao.text)
            except:
                print('Erro')
                pass
        resultados = driver.find_elements(By.CLASS_NAME, 'base-card')
        if len(lista_descricoes) == len(resultados):
            break
    descricao_salvar = '\n'.join(lista_descricoes)
    with open('descricoes_vagas.txt','w',encoding='utf-8') as f:
        f.write(descricao_salvar)
    driver.quit()
