# CROWLING

```python
from selenium.common import TimeoutException
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from undetected_chromedriver import Chrome, ChromeOptions
import selenium

# 대기 시간 1초
LOADING_WAIT_TIME = 5
# 크롤링할 상품 코드
pcodes = ['18853079']
# 결과 리스트
result = []

def init_driver():
    options = ChromeOptions()
    options.add_argument('--headless')
    options.add_argument('--disable-gpu')
    driver = Chrome(options=options)
    return driver

def find_review(pcode, driver):
    url = f'<http://prod.danawa.com/info/?pcode={pcode}>'
    driver.get(url)

    try:
        WebDriverWait(driver, LOADING_WAIT_TIME).until(
            EC.element_to_be_clickable(
                (By.XPATH, '//*[@id="danawa-prodBlog-productOpinion-button-tab-companyReview"]')
            )
        ).click()
    except TimeoutException:
        print("Could not find the review button.")
        return

    for i in range(1, 1000):
        try:
            WebDriverWait(driver, LOADING_WAIT_TIME).until(
                EC.visibility_of_element_located(
                    (By.CLASS_NAME, 'atc')
                )
            )
            for review in driver.find_elements(By.CLASS_NAME, 'atc'):
                result.append(review.text)
        except TimeoutException:
            print(f"Reviews on page {i} not found.")
            break

        if i % 10 == 0:
            right_btn = driver.find_element(By.XPATH, '//*[@class="mall_review"]//span[@class="point_arw_r"]')
            if right_btn.value_of_css_property('cursor') == 'pointer':
                right_btn.click()
            else:
                break
        else:
            try:
                driver.find_element(By.XPATH,
                                    f'//*[@id="danawa-prodBlog-companyReview-content-list"]/div/div/div/a[text()={i + 1}]'
                                    ).click()
            except:
                break

if __name__ == "__main__":
    driver = init_driver()
    for pcode in pcodes:
        find_review(pcode, driver)
    print(len(result))
    for r in result:
        print(r)

```

```python
from selenium.common.exceptions import StaleElementReferenceException, TimeoutException
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
import undetected_chromedriver as uc
import csv

# 대기 시간 3초 (필요에 따라 조절)
LOADING_WAIT_TIME = 3

# 크롤링할 상품 코드
pcodes = ['depth3=1']

# 결과 딕셔너리
product_data = dict()

def init_driver():
    driver = uc.Chrome(use_subprocess=True, auto_quit=False)
    return driver

def find_review(pcode, driver):
    url = f'https://cu.bgfretail.com/product/product.do?category=product&depth2=4&{pcode}'
    driver.get(url)

    while True:
        try:
            more_button = WebDriverWait(driver, LOADING_WAIT_TIME).until(
                EC.presence_of_element_located((By.XPATH, '//a[contains(text(), "더보기")]'))
            )
            more_button.click()
        except StaleElementReferenceException:
            continue
        except TimeoutException:
            break

    product_elements = driver.find_elements(By.CLASS_NAME, 'prod_wrap')
    for product_element in product_elements:
        name_element = product_element.find_element(By.CLASS_NAME, 'name')
        price_element = product_element.find_element(By.CLASS_NAME, 'price')
        img_element = product_element.find_element(By.TAG_NAME, 'img')

        product_name = name_element.text[2:]
        product_price = price_element.text[:-1]
        product_img_src = img_element.get_attribute('src')

        # 딕셔너리에 상품 이름, 가격, 이미지 주소 추가
        if product_name not in product_data:
            product_data[product_name] = {'가격': product_price, '이미지 주소': product_img_src}
        else:
            # 이미 상품이 딕셔너리에 있는 경우, 가격과 이미지 주소 업데이트
            product_data[product_name]['가격'] = product_price
            product_data[product_name]['이미지 주소'] = product_img_src

if __name__ == "__main__":
    driver = init_driver()
    for pcode in pcodes:
        find_review(pcode, driver)

    # 결과 딕셔너리를 CSV 파일로 저장
    with open('저장.csv', 'w', newline='') as csvfile:
        fieldnames = ['상품명', '가격', '이미지 주소']
        writer = csv.DictWriter(csvfile, fieldnames=fieldnames)

        writer.writeheader()
        for name, data in product_data.items():
            writer.writerow({'상품명': name, '가격': data['가격'], '이미지 주소': data['이미지 주소']})

    # 웹 드라이버 종료
    driver.quit()
```
