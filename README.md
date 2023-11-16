# Configuração do Ambiente de Desenvolvimento para Componentes Decidim

Antes de começarmos, este guia assume que você está desenvolvendo componentes para a versão 0.27 do Decidim. Utilizaremos Docker para configurar o ambiente de desenvolvimento.

## Passo 1: Clonar este repositório
```bash
git clone https://gitlab.com/lappis-unb/decidimbr/components-brasil-participativo/template-component
```

A estrutura de arquivos após este passo será:
```plaintext
.
├── docker-compose.yml
├── Dockerfile
└── README.md
```

## Passo 2: Clonar o repositório do Decidim
Na raiz do template do componente, clone o repositório do Decidim:
```bash
git clone https://github.com/decidim/decidim.git
```

A estrutura de arquivos após este passo será:
```plaintext
├── decidim
├── docker-compose.yml
├── Dockerfile
└── README.md
```

## Passo 3: Subir o ambiente de desenvolvimento
```bash
docker-compose up -d
docker exec -it lappis_ws_decidim_server bash
```

## Passo 4: Criar o bundle da aplicação
```bash
bundle install
bin/rake development_app
```

Durante o processo do `rake`, um seed geral do Decidim será gerado.

## Passo 5: Rodar a aplicação
```bash
rails s -b 0.0.0.0 -p 3000
```

## Passo 6: Login
Após a conclusão do Passo 4, utilize as seguintes credenciais para fazer login:
```plaintext
email: admin@example.org 
senha: decidim123456789
```

Após seguir esses passos, o ambiente de desenvolvimento estará configurado e pronto para uso. 

---

**Terminologia:**
- **Docker:** Uma plataforma para desenvolvimento, envio e execução de aplicativos em contêineres. Contêineres permitem que uma aplicação e suas dependências sejam empacotadas juntas.
  
- **Docker Compose:** Uma ferramenta para definir e executar aplicativos Docker multi-container. O arquivo `docker-compose.yml` neste projeto descreve os serviços, redes e volumes necessários para o ambiente Decidim.

- **Bundle:** É uma ferramenta para gerenciar as dependências de um projeto Ruby. O comando `bundle install` instala as gemas (bibliotecas Ruby) necessárias para o projeto.

- **Rake:** Uma ferramenta de construção de software semelhante ao Make, escrita em Ruby. No contexto deste projeto, `bin/rake development_app` é usado para criar o aplicativo Decidim para o ambiente de desenvolvimento.

- **Rails:** Um framework de desenvolvimento web em Ruby. O comando `rails s -b 0.0.0.0 -p 3000` inicia o servidor web para executar a aplicação Decidim.

Espero que essas explicações ajudem a entender melhor o processo de configuração do ambiente de desenvolvimento para os componentes do Decidim.