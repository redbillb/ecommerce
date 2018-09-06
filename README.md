# udemy_django
Curso da Udemy e-commerce com Djando e Testes



Step 1:
To check if you have Anaconda installed, open a Windows command prompt (winkey+r, type “cmd” and hit “OK”), type

conda -V
and hit enter. If no error is returned, Anaconda is installed.

I recommend a clean install of Anaconda, especially if you tried to manually install Python before installing Anaconda. 
Windows is not forgiving when it comes to messing with paths/dependencies/etc., so if you have any issues with the remainder 
of this tutorial, I recommend uninstalling Anaconda, making sure there are no Python distributions in your 
C:\ drive, then clean-installing Anaconda.

You can download the Anaconda installer here. It doesn’t really matter what version of Python you choose to install 
with Anaconda , since you can always create a virtual environment with an older version. However, I would recommend 
installing the most up-to-date distribution because it’s generally better to be on the curve than behind it.


Step 2: Check conda is up-to-date
If you haven’t yet, open a Windows command prompt. Enter the following command

conda update conda
then enter “y” if prompted to accept the packages that need to be updated.


Step 3: Create your virtual environments
conda create -n python35 python=3.5 anaconda

conda info -e
mostra os ambientes criados


Step 4:
para acessar um dos ambientes virtuais
activate python35


Step 5:
instalar bibliotecas adicionais:
pip install django==1.9.5
pip install msgpack (para satisfazer o pip)
python -m pip install --upgrade pip (para atualizar o pip)


Step 6:
django-admin startproject ecommerce
para criar o diretorio 'ecommerce' com a estrutura necessaria para o projeto


Step 7:
entrar no diretorio do projeto ecommerce e executar:
python manage.py runserver 0.0.0.0:8000 (libear para ser acessado de qualquer ponto da rede e especificar a porta)
acessar a web
http://localhost:8000/  (se for acessar de outra maquina trocar 'localhost' pelo ip do servidor

ver retorno:
It worked!
Congratulations on your first Django-powered page.
Tudo certo com as instalaçoes e com o servidor.


Step 8:
ajustes iniciais no arquivos de configuraçoes da aplicação
settings.py

alterando o seguinte:
LANGUAGE_CODE = 'pt-br'

TIME_ZONE = 'America/Recife'

ajustar o banco de dados a ser utilizado caso seja necessario alterar:
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    }


Step 9:
A aplicacao sera dividida em aplicaçoes menores
Criar a aplicação 'core'. Dentro do diretorio base da nossa app executar:
python manage.py startapp core



step 10:
Para utilizar arquivos staticos com o djnago(em ambiente de desenvolvimento ou aplicaçoes pequenas)
-criar pasta static dentro da aplicaçao core
-colocar os arquivos nessa pasta
-garantir as tres configuraçoes abaixo no arquivo settings.py
-executar por meio do 'runserver'

1-
STATIC_URL = '/static/' (no final do arquivo)

2-
'django.contrib.staticfiles', (na seção de aplicaçoes)

3-
DEBUG = True

para ver se esta funcionando acessar pelo navegador
http://localhost:8000/static/assets/bootstrap.min.css (nesse caso os arquivos estao dentro da pasta 'static/assets')

acrescentar {% load static %}
fazer ajustes nas linhas de chamada dos arquivos
de
href="assets/bootstrap.min.css'"
para
href="{% static 'assets/bootstrap.min.css' %}"


Step 11:
Para definir templates:
template base:
trocar o que vai ser altrado por
{% block container %}{% endblock %}

e criar um templete para cada uso(produtos, lista de produtos, contato) nesses templetes colocar o html dentro de:
{% extends "base.html" %}

{% block title %}
    Contato | {{ block.super }}
{% endblock %}

{% block container %}
####html aqui#####
{% endblock %}


Testes
ao inves de usar o arquivo tests.py criado pelo django, 
   remover esse arquivo, 
   criar pasta tests
   criar arquivo init
   criar arquivos de teste(uma para cada item exemplo: test_views.py)

para executar os testes:
python manage.py test

