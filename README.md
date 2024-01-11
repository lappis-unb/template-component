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

## Passo 3: Alterar a versão para a 0.27

```bash
cd decidim
git checkout release/0.27-stable
cd ..
```

## Passo 4: Subir o ambiente de desenvolvimento

```bash
docker-compose up -d
docker exec -it lappis_ws_decidim_server bash
```

## Passo 5: Criar o development_app (~25min)

Atualize o bundler:

```bash
gem install bundler:2.3.20
bundle update --bundler
```

Crie o development_app

```bash
bundle install
bin/rake development_app
```

Durante o processo do `rake`, um seed geral do Decidim será gerado.

## Passo 6: Rodar a aplicação

```bash
cd development_app
bin/rails s -b 0.0.0.0 -p 3000
```

## Passo 7: Login

Após a conclusão do Passo 4, utilize as seguintes credenciais para fazer login:

```plaintext
email: admin@example.org 
senha: decidim123456789
```

Após seguir esses passos, o ambiente de desenvolvimento estará configurado e pronto para uso. 

# Criando um componente

## Passo 1: Instalando dependencias

```bash
gem install decidim-generators
```

## Passo 2: Gerando componente

⚠ O nome do componente precisa estar no plural ou ser o topo de alguma hierarquia ⚠

```bash
decidim --component <nome_do_componente>
```

## Passo 3: Adicionando o componente no `Gemfile`

```bash
cd development_app
```

Abra o arquivo `Gemfile` e adicione a seguinte linha:

```
gem "decidim-<nome_do_componente>", path: ".."
```

Agora basta instalar a Gem:

```bash
bundle install
```

## Passo 4: Permitir a edicao do componente fora do docker

Entre pelo terminal dentro do diretorio do `template-component` e de o seguinte comando:

```bash
sudo chown -R <seu_usuario>:<seu_usuario> decidim/
```

# Configurando o componente

## Passo 1: 


# Informacoes importantes

## Atualizando development_app

Apos criar um novo db dentro do seu componente voce precisa rodar o seguinte codigo dentro de `development_app`:

```bash
bin/rails decidim:upgrade
bin/rails db:migrate
```


---

**Terminologia:**
- **Docker:** Uma plataforma para desenvolvimento, envio e execução de aplicativos em contêineres. Contêineres permitem que uma aplicação e suas dependências sejam empacotadas juntas.
  
- **Docker Compose:** Uma ferramenta para definir e executar aplicativos Docker multi-container. O arquivo `docker-compose.yml` neste projeto descreve os serviços, redes e volumes necessários para o ambiente Decidim.

- **Bundle:** É uma ferramenta para gerenciar as dependências de um projeto Ruby. O comando `bundle install` instala as gemas (bibliotecas Ruby) necessárias para o projeto.

- **Rake:** Uma ferramenta de construção de software semelhante ao Make, escrita em Ruby. No contexto deste projeto, `bin/rake development_app` é usado para criar o aplicativo Decidim para o ambiente de desenvolvimento.

- **Rails:** Um framework de desenvolvimento web em Ruby. O comando `rails s -b 0.0.0.0 -p 3000` inicia o servidor web para executar a aplicação Decidim.

Espero que essas explicações ajudem a entender melhor o processo de configuração do ambiente de desenvolvimento para os componentes do Decidim.