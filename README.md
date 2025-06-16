# Scraping-sencillo-de-Wikipedia
Script en Python que descarga una página de Wikipedia, extrae encabezados h2 y enlaces usando BeautifulSoup, e imprime los resultados ordenados. Ideal para aprender web scraping básico.
# Requisitos
Python 3.x

requests

beautifulsoup4

Puedes instalar las librerías necesarias con:

bash
Copiar
Editar
pip install requests beautifulsoup4
Uso
Ejecuta el script para ver los encabezados h2 y los enlaces extraídos de la página de Wikipedia:

python
Copiar
Editar
import requests
from bs4 import BeautifulSoup

# Descargar la página
url = 'https://en.wikipedia.org/wiki/Web_scraping'
response = requests.get(url)

# Procesar HTML
soup = BeautifulSoup(response.text, 'html.parser')

# Extraer encabezados h2
headings = [heading.text.strip() for heading in soup.find_all('h2')]

# Extraer enlaces href (filtrando None y anclas)
links = [link.get('href') for link in soup.find_all('a') if link.get('href') and link.get('href').startswith('http')]

# Imprimir resultados ordenados
print("Encabezados h2:")
for h in sorted(headings):
    print(f"- {h}")

print("\nEnlaces encontrados:")
for l in sorted(set(links)):
    print(f"- {l}")
