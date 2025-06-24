Marketplace de Energia Solar com Reflex

Reflex é uma biblioteca poderosa para construir aplicações web full-stack puras em Python. Este projeto visa desenvolver um marketplace de energia solar completo, conectando consumidores a empresas e serviços na área de energia solar.
Recursos Principais

    Python Puro: Desenvolva todo o frontend e backend da sua aplicação em Python, eliminando a necessidade de aprender Javascript.

    Flexibilidade Total: Comece rapidamente com Reflex e escale para aplicações complexas e ricas em recursos.

    Implantação Instantânea: Após a construção, implante sua aplicação com um único comando ou hospede-a em seu próprio servidor.

    Otimizado para SEO: Estrutura de URL amigável, meta tags dinâmicas e marcação Schema.org para alta visibilidade em mecanismos de busca.

    Foco na Conversão de Leads: Fluxos de usuário simplificados, CTAs proeminentes e formulários otimizados para maximizar a geração de leads.

Consulte nossa página de arquitetura para saber como o Reflex funciona internamente.
⚙️ Instalação

Abra um terminal e execute (Requer Python 3.10+):

pip install reflex

🥳 Crie sua primeira aplicação

A instalação do reflex também instala a ferramenta de linha de comando reflex.

Teste se a instalação foi bem-sucedida criando um novo projeto. (Substitua my_solar_marketplace pelo nome do seu projeto):

mkdir my_solar_marketplace
cd my_solar_marketplace
reflex init

Este comando inicializa um aplicativo de template em seu novo diretório.

Você pode executar este aplicativo em modo de desenvolvimento:

reflex run

Você deverá ver seu aplicativo rodando em http://localhost:3000.

Agora você pode modificar o código-fonte em my_solar_marketplace/my_solar_marketplace.py. O Reflex possui atualizações rápidas, então você pode ver suas alterações instantaneamente ao salvar seu código.
Sequência de Prompts para Copilot: Desenvolvimento de Marketplace de Energia Solar com Reflex

Este documento lista todos os prompts em ordem estrita que você, como "Copilot", deve seguir para construir o marketplace de energia solar utilizando o Reflex Framework. Cada prompt é uma instrução clara, objetiva e detalhada, visando uma implementação passo a passo.

Instruções Gerais para o Copilot:

    Linguagem: O código deve ser em Python, utilizando o Reflex Framework.

    Banco de Dados: Interaja com o PostgreSQL via modelos ORM (SQLModel/SQLAlchemy) conforme a estrutura definida.

    Modularidade: Mantenha os componentes e estados pequenos e focados.

    Responsividade: Todos os componentes de UI devem ser responsivos para desktop e mobile.

    Validação: Implemente validação de formulário tanto no frontend (usando atributos Reflex) quanto no backend (no rx.State methods).

    Feedback ao Usuário: Sempre forneça feedback claro (sucesso, erro, carregamento) usando rx.toast, rx.alert ou estados visuais.

    SEO: Preste atenção às URLs, meta tags e estrutura HTML para SEO conforme especificado.

Fase 1: Configuração e Autenticação Base
Prompt 1.1: Configuração Inicial do Projeto Reflex e Modelos ORM

Tarefa: Inicialize um novo projeto Reflex e defina todos os modelos ORM (SQLModel) para o banco de dados PostgreSQL.

Especificações:

    Criação do Projeto: Crie um novo projeto Reflex.

    Configuração do DB: Configure rxconfig.py para usar PostgreSQL.

    Modelos ORM:

        Crie arquivos Python para os modelos.

        Defina as classes de modelo (herde de SQLModel e table=True) para as seguintes tabelas, com seus campos e tipos de dados conforme o plano:

            User (com user_type, company_id, profile_image_url)

            Company

            CompanyService

            CompanyProject

            QuotationRequest

            AdCampaign

            Payment

            Category

            Product (se usado)

            Review

            Lead

            Impression

            Message

            Object

            Bucket

        Adicione relacionamentos (Relationship) onde apropriado (ex: User.company, Company.services).

    Base App: Crie um index.py com uma página inicial mínima e um _app.py básico.

Código Esperado (Estrutura):

my_solar_marketplace/
├── my_solar_marketplace.py (ou index.py)
├── rxconfig.py
├── models/
│   ├── __init__.py
│   ├── user.py (com User model)
│   ├── company.py (com Company, CompanyService, CompanyProject models)
│   ├── marketplace.py (com QuotationRequest, AdCampaign, Payment, Review, Lead, Impression, Message models)
│   ├── content.py (com Category, Product models)
│   └── storage.py (com Object, Bucket models)
└── assets/

Comandos e Prompts para Copilot:

# Copilot, inicie um novo projeto Reflex chamado 'my_solar_marketplace'.
reflex init my_solar_marketplace
cd my_solar_marketplace

# Copilot, configure 'rxconfig.py' para usar PostgreSQL.
# Adicione a seguinte configuração ao 'rxconfig.py':
# config = rx.Config(
#     app_name="my_solar_marketplace",
#     db_url="postgresql://user:password@host:port/database",
#     env=rx.Env.DEV,
# )

# Copilot, crie o diretório 'models' e seus arquivos Python para os modelos ORM.
mkdir my_solar_marketplace/models
touch my_solar_marketplace/models/__init__.py
touch my_solar_marketplace/models/user.py
touch my_solar_marketplace/models/company.py
touch my_solar_marketplace/models/marketplace.py
touch my_solar_marketplace/models/content.py
touch my_solar_marketplace/models/storage.py

# Copilot, adicione o conteúdo dos modelos ORM conforme a estrutura de banco de dados fornecida.
# Para my_solar_marketplace/models/user.py:
# (Incluir a classe User com campos e relacionamentos)
# Para my_solar_marketplace/models/company.py:
# (Incluir as classes Company, CompanyService, CompanyProject com campos e relacionamentos)
# Para my_solar_marketplace/models/marketplace.py:
# (Incluir as classes QuotationRequest, AdCampaign, Payment, Review, Lead, Impression, Message com campos e relacionamentos)
# Para my_solar_marketplace/models/content.py:
# (Incluir as classes Category, Product com campos e relacionamentos)
# Para my_solar_marketplace/models/storage.py:
# (Incluir as classes Object, Bucket com campos e relacionamentos)

# Copilot, crie um 'index.py' básico e um '_app.py' no diretório raiz do projeto.
# my_solar_marketplace/my_solar_marketplace.py (ou index.py):
# import reflex as rx
# def index():
#     return rx.center(rx.text("Bem-vindo ao Solar Marketplace!"))
# app = rx.App()
# app.add_page(index)

# my_solar_marketplace/_app.py (se a estrutura do template incluir):
# import reflex as rx
# def base_page(component):
#     return rx.chakra.vstack(
#         rx.chakra.heading("Meu Solar Marketplace", font_size="2em"),
#         component,
#         width="100%",
#     )

# Copilot, execute as migrações iniciais do banco de dados.
reflex db init
reflex db migrate -m "Initial models creation"
reflex db upgrade head

Prompt 1.2: Implementação do Estado e Lógica de Autenticação

Tarefa: Crie o estado global de autenticação (AuthState) e implemente os métodos de registro, login e logout.

Especificações:

    AuthState: Crie state/auth.py e defina class AuthState(rx.State):.

        Variáveis de Estado: is_authenticated: bool = False, user: Optional[User] = None, error_message: str = "".

        Método on_load(): Tente carregar o usuário autenticado na inicialização.

    handle_register(form_data: dict):

        Recebe email, password, user_type (de form_data).

        Valida os dados.

        Cria um novo User no banco de dados.

        Define is_authenticated = True e user = novo_usuario em caso de sucesso.

        Define error_message em caso de falha (e-mail já existe, etc.).

        Use rx.redirect("/") ou rx.redirect("/dashboard") dependendo do user_type.

    handle_login(form_data: dict):

        Recebe email, password.

        Verifica credenciais no DB.

        Define is_authenticated = True e user = usuario_logado.

        Define error_message em caso de falha.

        Use rx.redirect("/") ou rx.redirect("/dashboard") dependendo do user_type.

    handle_logout():

        Limpa o estado de autenticação (is_authenticated = False, user = None).

        Redireciona para a página de login (rx.redirect("/login")).

    Database Interaction: Utilize operações de DB (SQLModel add, query, commit) dentro dos métodos do AuthState.

Código Esperado (Estrutura):

my_solar_marketplace/
└── state/
    └── auth.py

Comandos e Prompts para Copilot:

# Copilot, crie o diretório 'state' e o arquivo 'auth.py'.
mkdir my_solar_marketplace/state
touch my_solar_marketplace/state/auth.py

# Copilot, implemente a classe AuthState em 'my_solar_marketplace/state/auth.py'
# com as variáveis de estado is_authenticated, user, error_message e os métodos handle_register, handle_login, handle_logout, e on_load.
# Certifique-se de importar o modelo User de models.user e SQLModel, Session, create_engine de sqlmodel.

# Exemplo de estrutura interna para AuthState:
# from sqlmodel import Field, Session, SQLModel, create_engine, select
# from my_solar_marketplace.models.user import User
# import reflex as rx
# from typing import Optional
#
# class AuthState(rx.State):
#     is_authenticated: bool = False
#     user: Optional[User] = None
#     error_message: str = ""
#
#     @rx.cached_var
#     def is_company_manager(self) -> bool:
#         return self.is_authenticated and self.user and self.user.user_type == "company_manager"
#
#     @rx.cached_var
#     def is_admin(self) -> bool:
#         return self.is_authenticated and self.user and self.user.user_type == "admin"
#
#     def on_load(self):
#         # Lógica para carregar o usuário autenticado da sessão, se existir
#         pass # Implementar com lógica de sessão Reflex
#
#     def handle_register(self, form_data: dict):
#         # Lógica de validação e criação de usuário no DB
#         pass
#
#     def handle_login(self, form_data: dict):
#         # Lógica de verificação de credenciais no DB
#         pass
#
#     def handle_logout(self):
#         # Lógica para limpar sessão e redirecionar
#         pass

Prompt 1.3: Criação das Páginas de Login e Registro

Tarefa: Desenvolva as interfaces de usuário para as páginas de login e registro, integrando-as com o AuthState.

Especificações:

    Página de Login (pages/login.py):

        Use rx.center, rx.vstack para layout.

        Componentes: rx.heading("Login"), rx.form, rx.form_control, rx.input(type="email"), rx.password(), rx.button("Entrar", type="submit").

        Integração: No on_submit do formulário, chame AuthState.handle_login.

        Exiba AuthState.error_message usando rx.alert se houver.

        Link para a página de registro.

    Página de Registro (pages/register.py):

        Similar ao login, com campos adicionais.

        Componentes: rx.heading("Registrar"), rx.input(type="email"), rx.password(), rx.password(placeholder="Confirme a Senha"), rx.select para user_type ("Consumidor", "Empresa").

        Validação Frontend: Adicione validação básica (senhas devem ser iguais) antes do on_submit.

        Integração: No on_submit do formulário, chame AuthState.handle_register.

        Exiba AuthState.error_message usando rx.alert.

        Link para a página de login.

    Roteamento: Adicione rotas para /login e /register em my_solar_marketplace/my_solar_marketplace.py (ou index.py).

UI/UX:

    Design limpo e focado nos formulários.

    Feedback visual imediato para entrada do usuário.

    Botões de submissão claros.

Comandos e Prompts para Copilot:

# Copilot, crie o diretório 'pages' e os arquivos 'login.py' e 'register.py'.
mkdir my_solar_marketplace/pages
touch my_solar_marketplace/pages/login.py
touch my_solar_marketplace/pages/register.py

# Copilot, implemente a UI da página de login em 'my_solar_marketplace/pages/login.py'.
# Certifique-se de importar AuthState e usar rx.form, rx.input, rx.password, rx.button, rx.link, e rx.alert para o erro.

# Copilot, implemente a UI da página de registro em 'my_solar_marketplace/pages/register.py'.
# Inclua campos para email, senha, confirmação de senha, e um rx.select para user_type.
# Adicione validação básica de senha no frontend antes de chamar handle_register.

# Copilot, adicione as rotas para /login e /register em 'my_solar_marketplace/my_solar_marketplace.py'.
# No arquivo principal (my_solar_marketplace/my_solar_marketplace.py):
# from my_solar_marketplace.pages.login import login_page
# from my_solar_marketplace.pages.register import register_page
#
# app.add_page(login_page, route="/login")
# app.add_page(register_page, route="/register")

Prompt 1.4: Proteção de Rotas e Redirecionamento Base

Tarefa: Implemente a lógica para proteger rotas específicas e redirecionar usuários com base no seu status de autenticação e tipo.

Especificações:

    _app.py: Modifique o arquivo _app.py (ou onde a lógica global de layout é definida).

    on_load Global: No rx.App ou no rx.State principal, utilize AuthState.on_load ou lógica equivalente para verificar o status de autenticação.

    Proteção de Dashboard:

        Se o usuário tentar acessar /dashboard (ou qualquer rota de empresa) e AuthState.user.user_type não for 'company_manager' ou 'admin', redirecione para / ou /login.

        Se o usuário tentar acessar qualquer rota protegida e AuthState.is_authenticated for False, redirecione para /login.

    Barra de Navegação Condicional:

        No cabeçalho (rx.chakra.HStack ou similar), exiba "Login" e "Registrar" se AuthState.is_authenticated for False.

        Exiba "Dashboard da Empresa" ou "Meu Perfil" e "Logout" se AuthState.is_authenticated for True.

UI/UX:

    Redirecionamentos suaves, sem flashes de conteúdo não autorizado.

    Navegação intuitiva baseada no status do usuário.

Comandos e Prompts para Copilot:

# Copilot, modifique o arquivo principal da aplicação (my_solar_marketplace/my_solar_marketplace.py ou _app.py)
# para incluir a lógica de proteção de rotas e navegação condicional.
# Importe AuthState.

# Adicione uma função de layout global ou modifique o _app.py para:
# def base_layout(component):
#     return rx.chakra.vstack(
#         rx.chakra.HStack(
#             rx.chakra.heading("Solar Marketplace"),
#             rx.chakra.spacer(),
#             rx.cond(
#                 AuthState.is_authenticated,
#                 rx.chakra.HStack(
#                     rx.cond(
#                         AuthState.is_company_manager | AuthState.is_admin,
#                         rx.link("Dashboard", href="/dashboard"),
#                     ),
#                     rx.button("Logout", on_click=AuthState.handle_logout),
#                 ),
#                 rx.chakra.HStack(
#                     rx.link("Login", href="/login"),
#                     rx.link("Registrar", href="/register"),
#                 ),
#             ),
#             width="100%",
#             padding="1em",
#             border_bottom="1px solid #eee",
#         ),
#         component,
#         width="100%",
#     )

# Aplique o layout global às páginas relevantes, por exemplo:
# app.add_page(index, route="/", title="Home", on_load=AuthState.on_load)
# app.add_page(dashboard_page, route="/dashboard", title="Dashboard", on_load=AuthState.on_load) # Proteger esta rota
# (Similar para outras páginas protegidas)

# Na função on_load de AuthState, adicione a lógica de redirecionamento:
# from reflex.utils import types
#
# if not self.is_authenticated:
#     if self.router.page.path not in ["/login", "/register", "/"]:
#         return rx.redirect("/login")
# else:
#     if self.router.page.path == "/login" or self.router.page.path == "/register":
#         return rx.redirect("/") # Ou para o dashboard se for empresa
#     if self.router.page.path.startswith("/dashboard") and not (self.user.user_type == "company_manager" or self.user.user_type == "admin"):
#         return rx.redirect("/")

Fase 2: Área Pública (Consumidores)
Prompt 2.1: Desenvolvimento da Página Inicial e Componente de Busca

Tarefa: Construa a página inicial pública com um componente de busca por empresas, incluindo filtros de localização.

Especificações:

    HomePageState(rx.State):

        Variáveis: search_query: str = "", selected_state: str = "", selected_city: str = "", companies_list: list[Company] = [], total_companies: int = 0, current_page: int = 1, items_per_page: int = 10.

        Métodos:

            on_load(): Chame fetch_companies() na carga inicial.

            fetch_companies(): Consulta o DB para Company com base em search_query, selected_state, selected_city, com paginação. Retorna lista de Company e total_companies.

            update_search_query(value: str): Atualiza search_query e chama fetch_companies().

            update_state_filter(value: str): Atualiza selected_state e chama fetch_companies().

            update_city_filter(value: str): Atualiza selected_city e chama fetch_companies().

            set_page(page_num: int): Atualiza current_page e chama fetch_companies().

    pages/index.py (HomePage UI):

        Hero Section: rx.center com rx.vstack contendo rx.heading("Encontre a Melhor Energia Solar para Você!"), e a barra de busca.

        Barra de Busca: rx.hstack contendo:

            rx.input(placeholder="Busque por empresa ou serviço...", on_change=HomePageState.update_search_query, debounce_timeout=500)

            rx.select(placeholder="Estado", items=list_of_states, on_change=HomePageState.update_state_filter)

            rx.select(placeholder="Cidade", items=list_of_cities_by_state, on_change=HomePageState.update_city_filter)

        Resultados da Busca: rx.grid para exibir os CompanyCard (veja prompt 2.1.3).

        Paginação: rx.chakra.Pagination componente abaixo dos resultados, integrado com HomePageState.set_page.

    Dados de Localização:

        Crie uma função Python para fornecer uma lista estática de estados brasileiros.

        Crie uma função que, dado um estado, retorne uma lista de cidades (pode ser estática ou carregada de um DB/API).

UI/UX:

    Layout responsivo para todos os tamanhos de tela.

    Barra de busca proeminente no topo da página.

    Filtros claros e intuitivos.

    Paginação visível e fácil de usar.

    SEO: URLs semânticas para resultados de busca (ex: /empresas?estado=SP&cidade=SaoPaulo).

Tasks para Copilot:

# Copilot, crie o arquivo 'state/home_page.py' e defina HomePageState.
touch my_solar_marketplace/state/home_page.py

# Copilot, implemente os métodos fetch_companies, update_search_query, update_state_filter, update_city_filter, set_page no HomePageState.
# Adicione a lógica para interagir com o modelo Company no banco de dados, aplicando filtros e paginação.
# Inclua funções auxiliares para 'list_of_states' e 'list_of_cities_by_state' que podem ser chamadas pelo estado.

# Copilot, crie o diretório 'components' e o arquivo 'company_card.py'.
mkdir my_solar_marketplace/components
touch my_solar_marketplace/components/company_card.py

# Copilot, desenvolva o componente CompanyCard(company: Company) em 'my_solar_marketplace/components/company_card.py'.
# Ele deve receber um objeto Company e exibir: logo (rx.image), nome (rx.heading), avaliação média (rx.text com rx.icon de estrelas), localização (rx.text), link para perfil.

# Copilot, no 'my_solar_marketplace/pages/index.py', monte a UI da página inicial conforme especificações.
# Use rx.vstack, rx.hstack para o layout da seção Hero e da barra de busca.
# Use rx.grid para exibir CompanyCard's (rx.foreach(HomePageState.companies_list, lambda company: CompanyCard(company))).
# Adicione o componente rx.chakra.Pagination e integre-o com HomePageState.set_page.
# Certifique-se de importar HomePageState e CompanyCard.

# Copilot, no 'my_solar_marketplace/my_solar_marketplace.py', adicione a rota para a HomePage.
# from my_solar_marketplace.pages.index import index as home_page
# app.add_page(home_page, route="/", title="Solar Marketplace", on_load=HomePageState.on_load)

Prompt 2.2: Criação da Página de Perfil da Empresa (Público)

Tarefa: Desenvolva a página detalhada para cada empresa, acessível publicamente, exibindo todas as informações, serviços, projetos e avaliações.

Especificações:

    CompanyProfilePageState(rx.State):

        Variáveis: company: Optional[Company] = None, services: list[CompanyService] = [], projects: list[CompanyProject] = [], reviews: list[Review] = [], is_quotation_modal_open: bool = False, quotation_form_data: dict = {}.

        Método on_load(): Obtenha o company_id da URL (self.router.page.params.get("company_id")).

        Método fetch_company_data(): Consulta o DB para a Company e seus services, projects, reviews usando o company_id.

        Método toggle_quotation_modal(): Abre/fecha o modal de orçamento.

        Método submit_quotation_request(form_data: dict): Salva nova QuotationRequest e Lead no DB. Envia notificação básica para a empresa.

    pages/company_profile.py (CompanyProfilePage UI):

        Layout Principal: rx.container, rx.vstack.

        Informações Principais: rx.hstack para logo, nome da empresa, avaliação média, endereço, telefone, site.

        Abas: rx.tabs para Sobre, Serviços, Projetos, Avaliações.

            Aba "Sobre": rx.text(company.description), rx.badge para certificações.

            Aba "Serviços": rx.list ou rx.grid para CompanyServices.

            Aba "Projetos": rx.chakra.SimpleGrid de rx.image com legendas para CompanyProjects.

            Aba "Avaliações": rx.foreach(CompanyProfilePageState.reviews, lambda review: ReviewCard(review)).

        Botão de Orçamento: rx.button("Solicitar Orçamento", on_click=CompanyProfilePageState.toggle_quotation_modal).

        Modal de Orçamento: rx.modal com QuotationForm (campos: nome, email, telefone, descrição do projeto, localização), integrado com submit_quotation_request.

    Componentes Auxiliares:

        ReviewCard(review: Review): Componente para exibir uma única avaliação.

UI/UX:

    Design limpo e responsivo.

    Navegação por abas intuitiva para diferentes seções do perfil.

    Formulário de orçamento acessível e fácil de preencher.

    Galeria de projetos visualmente atraente.

    SEO: URLs como /empresa/[nome-da-empresa-slug], meta tags dinâmicas para o perfil da empresa, Schema.org (LocalBusiness).

Tasks para Copilot:

# Copilot, crie o arquivo 'state/company_profile_page.py' e defina CompanyProfilePageState.
touch my_solar_marketplace/state/company_profile_page.py

# Copilot, implemente fetch_company_data, toggle_quotation_modal, submit_quotation_request em CompanyProfilePageState.
# Garanta que fetch_company_data obtenha o company_id da URL e consulte todos os dados relacionados (services, projects, reviews).
# Implemente a lógica para salvar QuotationRequest e Lead no DB.

# Copilot, crie o arquivo 'pages/company_profile.py'.
touch my_solar_marketplace/pages/company_profile.py

# Copilot, desenvolva a UI da página 'my_solar_marketplace/pages/company_profile.py' usando rx.tabs e outros componentes.
# Inclua o layout principal, informações da empresa, abas para serviços, projetos e avaliações.
# Para a aba de projetos, use rx.chakra.SimpleGrid de rx.image com legendas.

# Copilot, crie o componente 'QuotationForm' (pode ser uma função separada ou um componente em 'components/').
# E integre-o no rx.modal dentro da página de perfil, chamando submit_quotation_request.

# Copilot, crie o componente 'ReviewCard' para exibir avaliações.
# Pode ser em 'components/review_card.py' ou diretamente em 'company_profile.py' se for simples.

# Copilot, configure a rota dinâmica '/empresa/[company_id]' (ou '/empresa/[company_slug]') para esta página em 'my_solar_marketplace/my_solar_marketplace.py'.
# Exemplo:
# from my_solar_marketplace.pages.company_profile import company_profile_page
# app.add_page(company_profile_page, route="/empresa/[company_id]", title="Perfil da Empresa", on_load=CompanyProfilePageState.on_load)

# Copilot, adicione lógica no CompanyProfilePageState para atualizar 'impressions' (tipo 'company', 'view') quando a página do perfil é carregada.
# Crie uma função para registrar uma impressão na tabela 'impressions'.

Prompt 2.3: Sistema de Avaliações (Consumidor)

Tarefa: Permitir que consumidores logados avaliem empresas através de um formulário de avaliação.

Especificações:

    ReviewState(rx.State):

        Variáveis: rating: int = 0, comment: str = "", target_company_id: Optional[UUID] = None, is_review_modal_open: bool = False, error_message: str = "".

        Métodos:

            set_rating(value: int): Atualiza rating.

            set_comment(value: str): Atualiza comment.

            open_review_modal(company_id: UUID): Abre o modal e define target_company_id.

            close_review_modal(): Fecha o modal.

            submit_review():

                Valida rating e comment.

                Verifica se Auth.is_authenticated e Auth.user_type == 'consumer'.

                Salva nova Review no DB (usando Auth.user.id como reviewer_user_id).

                Atualiza Company.average_rating e Company.total_reviews para a empresa avaliada.

                Exibe rx.toast de sucesso ou error_message.

    UI do Formulário de Avaliação:

        rx.modal que é ativado por ReviewState.is_review_modal_open.

        Componentes dentro do modal: rx.heading("Avaliar Empresa"), rx.hstack de rx.icon (estrelas) para seleção de rating (0-5), rx.text_area para comment, rx.button("Enviar Avaliação", on_click=ReviewState.submit_review).

        Botão "Avaliar Empresa" na página de perfil da empresa, chamando ReviewState.open_review_modal(company.id).

UI/UX:

    Modal de avaliação limpo e fácil de preencher.

    Seleção visual de estrelas intuitiva.

    Feedback claro após o envio da avaliação.

Tasks para Copilot:

# Copilot, crie o arquivo 'state/review_state.py' e defina ReviewState.
touch my_solar_marketplace/state/review_state.py

# Copilot, implemente os métodos set_rating, set_comment, open_review_modal, close_review_modal, submit_review em ReviewState.
# Certifique-se de que submit_review interaja com os modelos Review e Company no banco de dados.

# Copilot, crie o componente 'ReviewFormModal' (ou adicione a lógica diretamente na página de perfil) utilizando rx.modal e seus componentes filhos para o formulário de avaliação.
# Integre a seleção de estrelas usando rx.hstack de rx.icon com on_click para set_rating.

# Copilot, adicione o botão "Avaliar Empresa" na CompanyProfilePage que chama ReviewState.open_review_modal(company.id).
# Este botão deve ser condicional, aparecendo apenas para usuários logados com user_type 'consumer'.

# Copilot, no submit_review do ReviewState, após o sucesso, chame CompanyProfilePageState.fetch_company_data() para re-renderizar as avaliações e a média na página de perfil.
# Isso garantirá que a página exiba a avaliação recém-adicionada e a média atualizada.

Fase 3: Área da Empresa (Dashboard de Gerenciamento)
Prompt 3.1: Dashboard da Empresa (Visão Geral)

Tarefa: Crie o painel de controle principal para empresas, exibindo métricas chave e links de navegação.

Especificações:

    CompanyDashboardState(rx.State):

        Variáveis: company_metrics: dict = {} (ex: {'total_leads': 0, 'profile_views': 0, 'avg_rating': 0, 'ad_spend': 0}).

        Método on_load(): Verifica se Auth.is_authenticated e Auth.user.user_type == 'company_manager'. Redireciona se não for.

        Método fetch_dashboard_metrics(): Consulta o DB para obter dados agregados de leads, impressions, reviews, ad_campaigns para a empresa logada (Auth.user.company_id).

    pages/dashboard/index.py (CompanyDashboardPage UI):

        Layout: rx.container, rx.vstack principal.

        Métricas: rx.chakra.SimpleGrid de rx.card (ou rx.box) contendo rx.stat para exibir as métricas: "Total de Leads", "Visualizações de Perfil", "Avaliação Média", "Gasto em Anúncios".

        Navegação Lateral/Superior: Um rx.drawer ou rx.chakra.HStack de rx.links para as seções de gerenciamento: "Meu Perfil", "Meus Serviços", "Meus Projetos", "Leads e Mensagens", "Campanhas de Anúncios".

UI/UX:

    Painel visualmente informativo, com métricas claras.

    Navegação intuitiva para as seções de gerenciamento.

    Layout responsivo.

Tasks para Copilot:

# Copilot, crie o diretório 'pages/dashboard' e o arquivo 'index.py'.
mkdir -p my_solar_marketplace/pages/dashboard
touch my_solar_marketplace/pages/dashboard/index.py

# Copilot, crie o arquivo 'state/company_dashboard.py' e defina CompanyDashboardState.
touch my_solar_marketplace/state/company_dashboard.py

# Copilot, implemente on_load com verificação de autenticação/tipo de usuário e fetch_dashboard_metrics em CompanyDashboardState.
# A lógica de fetch_dashboard_metrics deve consultar as tabelas leads, impressions, reviews, ad_campaigns para a empresa do usuário logado.

# Copilot, desenvolva a UI da página 'my_solar_marketplace/pages/dashboard/index.py'.
# Use rx.chakra.SimpleGrid de rx.card com rx.stat para exibir as métricas de CompanyDashboardState.company_metrics.

# Copilot, crie um componente de navegação (components/company_navbar.py ou similar) com links para as rotas do dashboard.
# Inclua este componente na CompanyDashboardPage.
touch my_solar_marketplace/components/company_navbar.py

# Copilot, adicione a rota /dashboard em 'my_solar_marketplace/my_solar_marketplace.py' e proteja-a para garantir acesso apenas a company_manager ou admin.
# Exemplo:
# from my_solar_marketplace.pages.dashboard.index import dashboard_page
# app.add_page(
#     dashboard_page,
#     route="/dashboard",
#     title="Dashboard da Empresa",
#     on_load=[AuthState.on_load, CompanyDashboardState.on_load], # Garanta que a verificação de autenticação ocorra
# )

Prompt 3.2: Gerenciamento do Perfil da Empresa

Tarefa: Permita que as empresas editem todos os detalhes do seu perfil público.

Especificações:

    CompanyProfileManagementState(rx.State):

        Variáveis: company_data: Optional[Company] = None, logo_file: Optional[list[File]] = None, logo_preview_url: str = "".

        Método on_load(): Carrega company_data para a empresa logada.

        Método handle_file_upload(file_list: list[File]): Gerencia o upload do logo (temporariamente ou direto para S3/objects). Define logo_preview_url.

        Método update_company_profile(form_data: dict):

            Recebe dados do formulário (name, description, address, phone, website_url, etc.).

            Atualiza o registro da Company no DB.

            Se houver logo_file, salva no objects e atualiza company.logo_url.

            Exibe rx.toast de sucesso ou erro.

    pages/dashboard/profile.py (CompanyProfileManagementPage UI):

        Layout: rx.vstack com rx.form.

        Campos de Formulário: rx.form_control, rx.input, rx.text_area, rx.select (para estado/cidade, categorias).

        Upload de Logo: rx.upload com on_upload=CompanyProfileManagementState.handle_file_upload, e rx.image para logo_preview_url.

        Botão Salvar: rx.button("Salvar Alterações", type="submit").

UI/UX:

    Formulário intuitivo com todos os campos de perfil.

    Pré-visualização do logo antes de salvar.

    Feedback de sucesso/erro.

Tasks para Copilot:

# Copilot, crie o arquivo 'state/company_profile_management.py'.
touch my_solar_marketplace/state/company_profile_management.py

# Copilot, implemente on_load, handle_file_upload, update_company_profile em CompanyProfileManagementState.
# Garanta que handle_file_upload utilize a tabela 'objects' para armazenamento e retorne a URL para preview.
# update_company_profile deve persistir as alterações no modelo Company.

# Copilot, crie o arquivo 'pages/dashboard/profile.py'.
touch my_solar_marketplace/pages/dashboard/profile.py

# Copilot, desenvolva a UI da página 'my_solar_marketplace/pages/dashboard/profile.py'.
# Popule os campos do formulário com CompanyProfileManagementState.company_data.
# Integre rx.upload para o campo de logo, exibindo logo_preview_url.
# O botão "Salvar Alterações" deve chamar CompanyProfileManagementState.update_company_profile.

# Copilot, adicione a rota /dashboard/profile em 'my_solar_marketplace/my_solar_marketplace.py' e proteja-a.
# Exemplo:
# from my_solar_marketplace.pages.dashboard.profile import company_profile_management_page
# app.add_page(
#     company_profile_management_page,
#     route="/dashboard/profile",
#     title="Gerenciar Perfil",
#     on_load=[AuthState.on_load, CompanyProfileManagementState.on_load],
# )

Prompt 3.3: Gerenciamento de Serviços e Projetos

Tarefa: Permita que as empresas adicionem, editem e removam seus serviços e projetos de portfólio.

Especificações:

    CompanyServicesState(rx.State):

        Variáveis: services_list: list[CompanyService] = [], is_service_modal_open: bool = False, current_service: Optional[CompanyService] = None.

        Métodos: on_load(), fetch_services(), open_service_modal(service_id=None), close_service_modal(), save_service(form_data: dict), delete_service(service_id: UUID).

    CompanyProjectsState(rx.State):

        Variáveis: projects_list: list[CompanyProject] = [], is_project_modal_open: bool = False, current_project: Optional[CompanyProject] = None, project_images_files: list[File] = [], project_images_preview_urls: list[str] = [].

        Métodos: on_load(), fetch_projects(), open_project_modal(project_id=None), close_project_modal(), handle_project_image_upload(file_list: list[File]), save_project(form_data: dict), delete_project(project_id: UUID).

    UI (pages/dashboard/services.py, pages/dashboard/projects.py):

        Listagens: rx.data_table para listar services_list e projects_list. Colunas com nome, descrição, ações (Editar, Excluir).

        Botões de Ação: rx.button("Adicionar Serviço", on_click=CompanyServicesState.open_service_modal()), rx.button("Adicionar Projeto", on_click=CompanyProjectsState.open_project_modal()).

        Modais de Formulário:

            ServiceModal: rx.modal com rx.form para CompanyService (título, descrição, categoria, faixa de preço).

            ProjectModal: rx.modal com rx.form para CompanyProject (título, descrição, localização, potência, data de conclusão, rx.upload para project_images_files e pré-visualização de project_images_preview_urls).

UI/UX:

    Tabelas de listagem claras e com opções de busca/filtro (opcional).

    Modais para adição/edição que não poluem a página principal.

    Upload de imagens fácil com pré-visualização para projetos.

Tasks para Copilot:

# Copilot, crie os arquivos 'state/company_services.py' e 'state/company_projects.py'.
touch my_solar_marketplace/state/company_services.py
touch my_solar_marketplace/state/company_projects.py

# Copilot, implemente os estados e métodos definidos para CompanyServicesState e CompanyProjectsState.
# Garanta que os métodos CRUD interajam corretamente com os modelos CompanyService e CompanyProject.
# handle_project_image_upload deve processar e salvar múltiplas imagens na tabela 'objects' e associar as URLs a CompanyProject.image_urls.

# Copilot, crie os arquivos 'pages/dashboard/services.py' e 'pages/dashboard/projects.py'.
touch my_solar_marketplace/pages/dashboard/services.py
touch my_solar_marketplace/pages/dashboard/projects.py

# Copilot, desenvolva a UI da página 'my_solar_marketplace/pages/dashboard/services.py' com rx.data_table para listar serviços e o ServiceModal para CRUD.

# Copilot, desenvolva a UI da página 'my_solar_marketplace/pages/dashboard/projects.py' com rx.data_table para listar projetos e o ProjectModal para CRUD.
# Implemente o rx.upload para imagens de projeto e a pré-visualização de múltiplas imagens.

# Copilot, adicione as rotas /dashboard/services e /dashboard/projects em 'my_solar_marketplace/my_solar_marketplace.py' e proteja-as.
# Exemplo:
# from my_solar_marketplace.pages.dashboard.services import services_page
# from my_solar_marketplace.pages.dashboard.projects import projects_page
# app.add_page(services_page, route="/dashboard/services", title="Meus Serviços", on_load=[AuthState.on_load, CompanyServicesState.on_load])
# app.add_page(projects_page, route="/dashboard/projects", title="Meus Projetos", on_load=[AuthState.on_load, CompanyProjectsState.on_load])

Prompt 3.4: Gerenciamento de Leads e Mensagens

Tarefa: Permita que as empresas visualizem as solicitações de orçamento (leads) e troquem mensagens com os consumidores.

Especificações:

    CompanyLeadsMessagesState(rx.State):

        Variáveis: leads_list: list[QuotationRequest] = [], messages_list: list[Message] = [], current_conversation_id: Optional[UUID] = None, reply_message_content: str = "".

        Métodos: on_load(), fetch_leads(), fetch_messages(), view_lead_details(lead_id: UUID), mark_lead_status(lead_id: UUID, status: str), select_conversation(conversation_id: UUID), send_reply().

    UI (pages/dashboard/leads_messages.py):

        Abas: rx.tabs para "Leads Recebidos" e "Mensagens".

        Aba "Leads Recebidos":

            rx.data_table para listar QuotationRequests (colunas: Solicitante, Serviço, Local, Status, Data).

            Ao clicar em um lead: rx.accordion ou rx.modal para exibir detalhes completos e campos para reply_message_content e rx.button("Enviar Resposta"), rx.select para mudar status.

        Aba "Mensagens":

            Listagem de conversas (rx.foreach de rx.hstacks para cada conversation_id).

            Ao selecionar uma conversa: rx.vstack exibindo todas as mensagens dessa conversation_id (messages_list), e um rx.text_area para reply_message_content com rx.button("Enviar").

UI/UX:

    Visualização clara e organizada de leads e mensagens.

    Facilidade para ver detalhes e responder diretamente.

    Indicadores visuais para leads/mensagens não lidas.

Tasks para Copilot:

# Copilot, crie o arquivo 'state/company_leads_messages.py'.
touch my_solar_marketplace/state/company_leads_messages.py

# Copilot, implemente todos os métodos em CompanyLeadsMessagesState para buscar, visualizar e interagir com leads e mensagens.
# Certifique-se de que fetch_leads e fetch_messages filtrem pelos leads/mensagens da empresa logada.

# Copilot, crie o arquivo 'pages/dashboard/leads_messages.py'.
touch my_solar_marketplace/pages/dashboard/leads_messages.py

# Copilot, desenvolva a UI da página 'my_solar_marketplace/pages/dashboard/leads_messages.py' com rx.tabs e rx.data_table.
# Implemente a lógica de exibição de detalhes do lead (usando rx.accordion ou um modal) e a interface de resposta.
# Implemente a interface de conversas na aba "Mensagens", permitindo selecionar e responder.

# Copilot, adicione a rota /dashboard/leads-messages em 'my_solar_marketplace/my_solar_marketplace.py' e proteja-a.
# Exemplo:
# from my_solar_marketplace.pages.dashboard.leads_messages import leads_messages_page
# app.add_page(
#     leads_messages_page,
#     route="/dashboard/leads-messages",
#     title="Leads e Mensagens",
#     on_load=[AuthState.on_load, CompanyLeadsMessagesState.on_load],
# )

Prompt 3.5: Gerenciamento de Campanhas de Anúncios e Pagamentos

Tarefa: Desenvolva o sistema completo para empresas criarem, gerenciarem e pagarem por campanhas de publicidade patrocinadas.

Especificações:

    AdCampaignsState(rx.State):

        Variáveis: campaigns_list: list[AdCampaign] = [], is_campaign_modal_open: bool = False, current_campaign: Optional[AdCampaign] = None, ad_image_file: Optional[File] = None, ad_image_preview_url: str = "".

        Métodos: on_load(), fetch_campaigns(), open_campaign_modal(campaign_id=None), close_campaign_modal(), handle_ad_image_upload(file_list: list[File]).

        Métodos CRUD para AdCampaign: save_campaign(form_data: dict), delete_campaign(campaign_id: UUID), pause_campaign(campaign_id: UUID), activate_campaign(campaign_id: UUID).

        Métodos de Rastreamento: track_ad_impression(campaign_id: UUID, event_type: str), track_ad_lead(campaign_id: UUID).

        Método initiate_payment(campaign_id: UUID, amount: float): Simula o processo de pagamento e salva em Payment.

    UI (pages/dashboard/ad_campaigns.py):

        Listagem de Campanhas: rx.data_table exibindo campaigns_list (colunas: Nome, Tipo, Período, Orçamento, Gastos, Cliques, Leads, Status, Ações).

        Botão "Criar Nova Campanha": rx.button(on_click=AdCampaignsState.open_campaign_modal()).

        CampaignModal: rx.modal com rx.form para AdCampaign.

        Campos básicos: campaign_name, campaign_type (rx.select), start_date (rx.date_picker), end_date (rx.date_picker), budget, target_url.

        Campos Condicionais (rx.cond):

            Se campaign_type for banner_ad ou popup_ad: rx.upload para ad_image_file e rx.image para ad_image_preview_url.

            Se campaign_type for ppc ou ppl: cpc_cpl_rate.

        Botões de Ação: "Salvar", "Pausar", "Ativar", "Excluir".

        Dashboard de Edição/Performance da Campanha (na mesma página ou modal): Exibe current_spend, total_clicks, total_leads para uma campanha selecionada.

        Botão "Pagar": Ativa AdCampaignsState.initiate_payment.

UI/UX:

    Interface intuitiva para criação e gerenciamento de campanhas.

    Dashboard de desempenho com métricas claras.

    Processo de pagamento simulado (ou integrado com API real).

    Visualização condicional de campos de formulário baseada no tipo de campanha.

Tasks para Copilot:

# Copilot, crie o arquivo 'state/ad_campaigns.py'.
touch my_solar_marketplace/state/ad_campaigns.py

# Copilot, implemente todos os métodos CRUD e de rastreamento (track_ad_impression, track_ad_lead) em AdCampaignsState.
# Garanta que a lógica de rastreamento atualize as tabelas 'impressions' e 'leads' conforme o tipo de evento.

# Copilot, crie o arquivo 'pages/dashboard/ad_campaigns.py'.
touch my_solar_marketplace/pages/dashboard/ad_campaigns.py

# Copilot, desenvolva a UI da página 'my_solar_marketplace/pages/dashboard/ad_campaigns.py' com rx.data_table para listar campanhas.
# Implemente o CampaignModal com os campos básicos e condicionais, integrando rx.upload para imagens de anúncios e sua pré-visualização.
# Desenvolva o dashboard de desempenho para campanhas individuais, mostrando métricas e botões de ação (Pausar, Ativar, Excluir).

# Copilot, implemente o método initiate_payment em AdCampaignsState para simular o registro de pagamentos na tabela payments.
# Use um rx.button "Pagar" para acionar este método.

# Copilot, adicione a rota /dashboard/ad-campaigns em 'my_solar_marketplace/my_solar_marketplace.py' e proteja-a.
# Exemplo:
# from my_solar_marketplace.pages.dashboard.ad_campaigns import ad_campaigns_page
# app.add_page(
#     ad_campaigns_page,
#     route="/dashboard/ad-campaigns",
#     title="Campanhas de Anúncios",
#     on_load=[AuthState.on_load, AdCampaignsState.on_load],
# )

Fase 4: Otimização e Refinamentos
Prompt 4.1: Otimização para SEO e Performance do Frontend

Tarefa: Implemente as otimizações de SEO e performance no frontend.

Especificações:

    URLs Amigáveis: Garanta que todas as rotas públicas utilizem slugs ou IDs amigáveis (/empresa/nome-da-empresa-slug, /empresas/estado/cidade).

    Meta Tags Dinâmicas:

        Na CompanyProfilePageState, defina o rx.head para usar company.name como <title> e company.description como <meta name="description">.

        Na HomePageState, defina <title> e <meta name="description"> com base nos filtros de busca (ex: "Empresas de Energia Solar em [Cidade] - [Estado]").

        Inclua Open Graph e Twitter Card tags para compartilhamento social.

    Schema.org Markup:

        Na CompanyProfilePage, adicione marcação Schema.org para LocalBusiness, Service, Review.

        Na HomePage, adicione marcação para WebSite ou SearchResultsPage.

    Lazy Loading:

        Utilize rx.lazy_load para componentes que não são visíveis inicialmente (ex: galerias de imagens de projetos que estão em uma aba separada, ou gráficos no dashboard).

    Otimização de Imagens: Garanta que imagens carregadas (logos, portfólio, banners) sejam salvas em formatos otimizados (WebP, JPEG comprimido) e servidas de forma eficiente (via objects).

Tasks para Copilot:

# Copilot, revise todas as definições de rota nos arquivos 'my_solar_marketplace.py' e outros, ajustando para URLs amigáveis com slugs (se aplicável).
# Por exemplo, /empresa/[company_slug] ao invés de /empresa/[company_id].

# Copilot, no CompanyProfilePageState e HomePageState, implemente a lógica de geração de rx.head com meta tags dinâmicas.
# Adicione tags <title>, <meta name="description">, Open Graph (og:title, og:description, og:image, og:url), e Twitter Card (twitter:card, twitter:title, twitter:description, twitter:image).

# Copilot, adicione a marcação Schema.org diretamente nos componentes de UI relevantes (usando atributos 'tag' e 'json_ld').
# Por exemplo, na CompanyProfilePage, adicione o JSON-LD para LocalBusiness, Service, Review.

# Copilot, identifique componentes adequados para rx.lazy_load e aplique-o.
# Por exemplo, envolva grandes galerias de imagens ou seções de gráficos com rx.lazy_load.

# Copilot, nos métodos handle_file_upload (para logo, projetos, anúncios), adicione lógica para compressão e conversão para formatos otimizados (como WebP ou JPEG comprimido) antes de salvar no 'objects' bucket.
# Isso pode exigir uma biblioteca de processamento de imagem Python (ex: Pillow).

Fase 5: Administração e Monitoramento
Prompt 5.1: Painel Administrativo Geral

Tarefa: Desenvolva um painel de administração para usuários com user_type = 'admin' gerenciarem a plataforma.

Especificações:

    AdminDashboardState(rx.State):

        Variáveis: active_tab: str = "companies", users_list: list[User] = [], companies_list: list[Company] = [], reviews_list: list[Review] = [], ad_campaigns_list: list[AdCampaign] = [].

        Métodos: on_load() (para verificação de admin), fetch_all_users(), fetch_all_companies(), fetch_all_reviews(), fetch_all_ad_campaigns().

        Métodos de Ação: toggle_user_active(user_id: UUID), toggle_company_active(company_id: UUID), approve_review(review_id: UUID), delete_entity(entity_type: str, entity_id: UUID).

    UI (pages/admin/index.py):

        Layout: rx.container com rx.vstack.

        Navegação por Abas: rx.tabs para "Usuários", "Empresas", "Avaliações", "Campanhas de Anúncios".

        Conteúdo das Abas:

            rx.data_table para listar cada tipo de entidade.

            Colunas devem incluir informações chave e botões de ação (ativar/desativar, aprovar/rejeitar, excluir, visualizar detalhes).

            Formulários modais para edição de detalhes (opcional, pode reutilizar formulários existentes).

        Logs e Auditoria: Link para uma página de logs (pages/admin/audit_logs.py).

UI/UX:

    Interface de gerenciamento clara e funcional.

    Tabelas paginadas e filtráveis.

    Botões de ação diretos para moderação.

Tasks para Copilot:

# Copilot, crie o diretório 'pages/admin' e o arquivo 'index.py'.
mkdir -p my_solar_marketplace/pages/admin
touch my_solar_marketplace/pages/admin/index.py

# Copilot, crie o arquivo 'state/admin_dashboard.py' e defina AdminDashboardState.
touch my_solar_marketplace/state/admin_dashboard.py

# Copilot, implemente todos os métodos de busca e ação em AdminDashboardState.
# Garanta que a verificação de admin ocorra em on_load.
# Os métodos de ação devem interagir com os modelos User, Company, Review, AdCampaign para realizar as operações de moderação.

# Copilot, desenvolva a UI da página 'my_solar_marketplace/pages/admin/index.py' com rx.tabs e rx.data_table's para cada entidade (Usuários, Empresas, Avaliações, Campanhas de Anúncios).
# Inclua botões de ação para ativar/desativar, aprovar/rejeitar e excluir.

# Copilot, proteja a rota /admin para acesso exclusivo de user_type = 'admin'.
# Exemplo em my_solar_marketplace.py:
# from my_solar_marketplace.pages.admin.index import admin_dashboard_page
# app.add_page(
#     admin_dashboard_page,
#     route="/admin",
#     title="Painel Administrativo",
#     on_load=[AuthState.on_load, AdminDashboardState.on_load],
#     # Adicione uma verificação específica para admin se AuthState.on_load não for suficiente.
# )

Prompt 5.2: Monitoramento e Relatórios Administrativos

Tarefa: Crie uma seção no painel administrativo para visualizar relatórios e métricas de alto nível da plataforma.

Especificações:

    AdminReportsState(rx.State):

        Variáveis: total_companies: int = 0, total_consumers: int = 0, total_leads_month: int = 0, total_ad_spend_month: float = 0, lead_conversion_rate: float = 0, top_performing_companies: list[Company] = [].

        Métodos: on_load(), fetch_platform_metrics().

    UI (pages/admin/reports.py):

        Layout: rx.vstack.

        Métricas Gerais: rx.chakra.SimpleGrid de rx.stat para exibir "Total de Empresas", "Total de Consumidores", "Leads no Mês", "Gasto Total em Anúncios", "Taxa de Conversão de Leads".

        Tabelas de Top: rx.data_table para "Empresas com Melhor Performance" (com base em leads ou avaliações) e "Campanhas Mais Lucrativas".

        Gráficos (Opcional, se houver wrapper Reflex para Chart.js/Recharts): Gráfico de linha de leads ao longo do tempo, gráfico de barras de categorias mais populares.

UI/UX:

    Relatórios claros e concisos.

    Visualização fácil de métricas importantes.

Tasks para Copilot:

# Copilot, crie o arquivo 'state/admin_reports.py'.
touch my_solar_marketplace/state/admin_reports.py

# Copilot, implemente fetch_platform_metrics em AdminReportsState para agregar dados das tabelas e calcular KPIs.
# As métricas devem ser obtidas de User, Company, Lead, AdCampaign, Payment, e Review.

# Copilot, crie o arquivo 'pages/admin/reports.py'.
touch my_solar_marketplace/pages/admin/reports.py

# Copilot, desenvolva a UI da página 'my_solar_marketplace/pages/admin/reports.py' para exibir as métricas e tabelas de top.
# Use rx.chakra.SimpleGrid de rx.stat para as métricas gerais.
# Use rx.data_table para as "Empresas com Melhor Performance" e "Campanhas Mais Lucrativas".

# Copilot, (Opcional) se houver um wrapper Reflex para bibliotecas de gráficos (como Recharts ou Chart.js), integre um gráfico de linha de leads ao longo do tempo ou um gráfico de barras de categorias mais populares.

# Copilot, adicione a rota /admin/reports em 'my_solar_marketplace/my_solar_marketplace.py' e proteja-a.
# Exemplo:
# from my_solar_marketplace.pages.admin.reports import admin_reports_page
# app.add_page(
#     admin_reports_page,
#     route="/admin/reports",
#     title="Relatórios Administrativos",
#     on_load=[AuthState.on_load, AdminReportsState.on_load],
# )

