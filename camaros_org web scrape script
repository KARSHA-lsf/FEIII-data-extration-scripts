from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.common.exceptions import TimeoutException
import time
import pandas as pd


driver = webdriver.Chrome()



# Wait 20 seconds for page to load
timeout = 20
parent_han  = driver.window_handles
try:
    compnay_name_data = []
    compnay_address_data = []
    
    trif_code = [22042, 69072 , 84791, 87089, 87081, 94036, 94031, 39269, 68029, 15091, 49019, 49111, 20057, 38011, 39011, 73269, 73089, 84281, 22041]
    
    for trf in trif_code:
        url ="http://directory.camaras.org/index.php?pagina=1&registros=0&offset=0&cocin=&impexp=EI&anno=17&tramo=00&empresa=&producto=TA&codprod="+str(trf)+"&areanacional=PR&codareanac=&areainternac=PS&codareainter="
        driver.get(url)
        links = driver.find_elements_by_xpath("//table[@class='modTb type2']//a[@class='link']")
        for link in links:
            link.click()
            driver.switch_to.window(driver.window_handles[1])
            WebDriverWait(driver, 10).until(EC.number_of_windows_to_be(2))
            all_han = driver.window_handles
            driver.switch_to.window(all_han[1])

            compnay_name = driver.find_element_by_xpath("//div[@class='modBox withTitle']/div/span").text
            comany_address_all = driver.find_elements_by_xpath("//div[@class='modBox withTitle']/ul[@class='ullis']/li")
            compnay_adress = comany_address_all[0].text +" "+comany_address_all[1].text
            compnay_name_data.append(compnay_name)
            compnay_address_data.append(compnay_adress)

            print compnay_name
            print compnay_adress
            time.sleep(2)
            driver.switch_to.window(all_han[0])
    d = {'compnay_name':compnay_name_data,'compnay_adress':compnay_address_data}
    camars_data = pd.DataFrame(d)
            #camars_data = pd.DataFrame({'compnay_name':compnay_name_data, 'compnay_adress':compnay_address_data},index=[0])
            
    camars_data.to_csv("camaras.org_companies_subset.csv",encoding = 'utf-8',sep='|',index=False)
    
    #print camars_data
        #WebDriverWait(driver, timeout).until(EC.visibility_of_element_located((By.XPATH, "//body[@class='popup']")))
except TimeoutException:
    print("Timed out waiting for page to load")
    driver.quit()

driver.close()
