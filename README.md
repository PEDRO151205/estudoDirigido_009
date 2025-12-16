# PATRI-TECH API

API REST para **inventário patrimonial**, construída com Django + Django REST Framework, documentada com **Swagger (drf-spectacular)** e com **controle de autenticação e permissões** adequadas a um MVP profissional.

---

## 📌 Visão Geral

O projeto fornece endpoints para gerenciar:

* **Categorias**
* **Status**
* **Unidades**
* **Salas**
* **Bens patrimoniais**

A API permite **leitura pública (GET)** e protege **operações de escrita (POST, PUT, PATCH, DELETE)** com autenticação.

----

## 🧱 Stack Tecnológica

* **Python 3.13+**
* **Django 5.x**
* **Django REST Framework (DRF)**
* **drf-spectacular** (Swagger / OpenAPI)
* **SQLite** (dev) — pode ser trocado por PostgreSQL em produção

---

## ⚙️ Instalação e Execução

1. Criar ambiente virtual e instalar dependências:

```bash
pip install django djangorestframework drf-spectacular
```

2. Aplicar migrações:

```bash
python manage.py migrate
```

3. Criar superusuário:

```bash
python manage.py createsuperuser
```

4. Iniciar o servidor:

```bash
python manage.py runserver
```

---

## 🔐 Autenticação e Permissões

### Estratégia adotada

* **GET**: acesso público
* **POST / PUT / PATCH / DELETE**: requer autenticação

Isso é implementado com:

* `TokenAuthentication`
* Permissão customizada baseada em métodos HTTP

### Obter Token

Endpoint:

```
POST /api/token/
```

Payload:

```json
{
  "username": "admin",
  "password": "sua_senha"
}
```

Resposta:

```json
{
  "token": "abc123..."
}
```

Use o token no header:

```
Authorization: Token abc123...
```

---

## 🌐 Endpoints da API

Base URL:

```
http://127.0.0.1:8000/api/
```

| Recurso    | Endpoint       |
| ---------- | -------------- |
| Categorias | `/categorias/` |
| Status     | `/status/`     |
| Unidades   | `/unidades/`   |
| Salas      | `/salas/`      |
| Bens       | `/bens/`       |

---

## 📘 Swagger (Documentação da API)

A documentação interativa está disponível em:

```
http://127.0.0.1:8000/docs/
```

### Funcionalidades do Swagger

* Listagem de todos os endpoints
* Testes diretos com **Try it out**
* Autenticação via botão **Authorize**
* Organização por **tags** (Categorias, Bens, etc.)

---

## 🎨 Customização do Swagger

### Título e Descrição

Configurados no `settings.py`:

```python
SPECTACULAR_SETTINGS = {
    "TITLE": "PATRI-TECH API",
    "DESCRIPTION": "API do sistema de inventário patrimonial",
    "VERSION": "1.0.0",
}
```

### Logo Personalizado

1. Criar arquivo CSS:

```
core/static/swagger/custom.css
```

2. Exemplo de CSS:

```css
.swagger-ui .topbar .swagger-ui-logo {
    display: none;
}

.swagger-ui .topbar {
    background-color: #0f172a;
}

.swagger-ui .topbar-wrapper::before {
    content: "";
    background-image: url("/static/swagger/logo.png");
    background-repeat: no-repeat;
    background-size: contain;
    height: 40px;
    width: 200px;
    display: block;
}
```

3. Colocar o logo em:

```
core/static/swagger/logo.png
```

4. Ativar no `settings.py`:

```python
SPECTACULAR_SETTINGS = {
    ...
    "SWAGGER_UI_SETTINGS": {
        "customCssUrl": "/static/swagger/custom.css",
    },
}
```

---

## 📋 Checklist de Conclusão

* [x] Modelos criados
* [x] Banco populado
* [x] Admin configurado
* [x] API REST funcionando
* [x] Autenticação implementada
* [x] Permissões por método HTTP
* [x] Swagger documentado
* [x] Logo e identidade visual

---

## 🚀 Próximos Passos

* Perfis de usuário (admin, operador, leitura)
* Auditoria (created_at, updated_at, created_by)
* Upload de imagens dos bens
* Geração de etiquetas (PDF / QR Code)
* Deploy em ambiente de produção

---

📌 **PATRI-TECH API** — base sólida para um backend profissional de inventário patrimonial.
