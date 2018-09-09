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

################
Step 5.5:
Criar no github um repositorio vazio com o noe da aplicação, copiar a url do repositorio
entrar no diretorio onde vai ser criado pelo git o diretorio do repositorio
eecutar git clone "url copiada do repositorio recem criado"
sera ciado um diretorio com o nome da aplicação"nome do repositorio no github"
esse passa a ser o diretorio base(diretorio de trabalho para essa aplicação)
################

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

Step 12:
Testes
ao inves de usar o arquivo tests.py criado pelo django, 
   remover esse arquivo, 
   criar pasta tests
   criar arquivo init
   criar arquivos de teste(uma para cada item exemplo: test_views.py)

para executar os testes:
python manage.py test

########
Step 13:
deploy no heroku
https://dashboard.heroku.com/apps

Acrecentar informaçoes na aplicação:
arquivos e conteudos:

- runtime.txt (arquivo que indica qual a versao do python vai ser usada para execução da aplicação)
   python-3.6.6


- requirements.txt (arfquivo que indica quais as bibliotecas e respectivas versoes devem ser intaladas para a app funcionar)
dj_database_url==0.4.2
Django==1.9.6
whitenoise==4.0
gunicorn==19.5
psycopg2==2.7


- Procfile (sem extensao mesmo, arquivo responssavel pela execução da app no heroku)
web: python manage.py runserver 0.0.0.0:$PORT


- LICENSE (pegar seu conteudo no github dessa app)

OBS: todos esses arquivos devem estar no dirbase, junto ao README.md

- arquivo settings.py (dentro do diretorio da app principal com o mesmo nome do diretorio superior)
  pegar alterações no github


- arquivo local_settings.py (dentro do diretorio da app principal com o mesmo nome do diretorio superior)
  pegar alterações no github
OBS: usado para sobrepor com informaçoes do deploy local, esse arquivo nao pode estar no github


- alterar o arquivo .gitignore para ignorar esse arquivo e nao leva-lo para o repositorio


- configurar o heroku para usar o repositorio do github


- instalar cliente do heroku no windows, logar nesse cliente


- cliar no botao "Deploy Branch" para que o heroku faça o deploy da aplicação


- acessar a aplicação pela web para confirmar que esta tudo correto


Step 14:
executar o migrate para executar a geração das diverssas bases de dados do django
python manage.py migrate(caso ja tenha sido executado nao fara nada)

depois disso fica acessivel a tela de login do admin do django
http://localhost:8000/admin/


Step 15:
Criando a aplicaçao que tem os modelos utilizados na app ecommerce
python manage.py startapp catalog
vamos altear o arquivo models.py dentro de catalog com os modelos da aplicação
incluir essa aplicação no arquivo settings.py na sessao INSTALLED_APPS

Step 16:
executar o makemigrations (para idenficar os modelos criados e preparar sua inclusao no banco)
python manage.py makemigrations

Step 17:
executar migrate novamente para que as tabelasa sejam criadas no banco de dados
python manage.py migrate 


Step18 :
Vamos utilizar o SqliteStudio para visualizar o banco de dados e as tabelas


Step19 :
Criar uma categiram um produto e interagir com eles
instalar o ipython (jupiter notebook sem interface web)
pip install ipython

utilizar assim:
python manage.py shell


Category.objects.create(name='Programação',slug='programacao') (criando uma categoria)

cat = Category.objects.all()[0]

Product.objects.create(name='Curso de Django', slup='curso-de-django',price=100,category=cat)

produto = Product.objects.all()[0]

produto.name (retorna o nomde do produto criado)
produto.category.name (retorna o nome da categoria do produto)


Step20 :
Criar usuario para acessar o /admin do django
python manage.py createsuperuser


Step21 :
aula 21 listando produtos(colocar ps comentarios a partir dessa aula)