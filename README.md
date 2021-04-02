# Web-Scraping-with-python
# Web Scrapping using request and request_html

import requests
from requests_html import HTML

# This fuction can be used for two websites(Vivo and iNeuron), link has been given below:

def web_Scraping(website_url, product):

    base_url = website_url
    product = product
    product = product.lower()

    if base_url == 'https://www.ineuron.ai/':
        product_url = f"{base_url}{product}"
        url = f"{base_url}home/{product}"
        r = requests.get(url)
        html_str = r.text
        html = HTML(html=html_str)
        product1 = html.find(".radio-custom-label")

        title1 = html.find(".side_title")
        print("Product URL: ", product_url, "\n")

        for i in range(1, len(product1)):
            if i < 55:
                product_in_product = product1[i].text
                product_in_product_lower = product_in_product.lower()
                product_in_product_rep = product_in_product_lower.replace(" ", "-")
                product_in_product_rep = product_in_product_rep.replace("+", "")
                product_in_product_rep = product_in_product_rep.replace("'", "")
                product_url = f"{base_url}home/{product}/{product_in_product_rep}/"

                print(product_in_product, "\n", product_url, "\n")

    elif base_url == 'https://www.vivo.com/in/':

        url = f"{base_url}{product}"
        r = requests.get(url)
        html_str = r.text
        html = HTML(html=html_str)
        product1 = html.find(".item.no-flip-over")
        print("Product URL: ", url, "\n")

        for i in range(1, len(product1)):
            model_name = product1[i].text
            model_name_lwr = model_name.lower()
            model_name_rpl = model_name_lwr.replace(" ", "")
            product_url = f"{base_url}{product}/{model_name_rpl}/"
            if model_name[0] == 'X':
                print("Model: ", "X Series")
                print(model_name, "\n", product_url, "\n")

            elif model_name[0] == 'V':
                print("Model: ", "V Series")
                print(model_name, "\n", product_url, "\n")

            elif model_name[0] == 'S':
                print("Model: ", "S Series")
                print(model_name, "\n", product_url, "\n")

            elif model_name[0] == 'Y':
                print("Model: ", "Y Series")
                print(model_name, "\n", product_url, "\n")

            elif model_name[0] == 'N':
                print("Model: ", "NEX Series")
                print(model_name, "\n", product_url, "\n")

            elif model_name[0] == 'Z':
                print("Model: ", "Z Series")
                print(model_name, "\n", product_url, "\n")

            elif model_name[0] == 'U':
                print("Model: ", "U Series")
                print(model_name, "\n", product_url, "\n")


# To change the url and product, uncomment website_url and product that you want
# and comment other website_url and product that you don't want

#website_url = 'https://www.ineuron.ai/'
#product = 'Courses'

website_url = 'https://www.vivo.com/in/'
product = 'products'

web_Scraping(website_url, product)
