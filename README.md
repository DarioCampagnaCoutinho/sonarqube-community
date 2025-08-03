# SonarQube Community - Deploy com Docker Compose (Produção)

Este projeto utiliza Docker Compose para orquestrar SonarQube, PostgreSQL e Nginx (proxy reverso) em ambiente de produção.

## Estrutura dos Serviços
- **nginx**: Proxy reverso, expõe a porta 80 para acesso externo.
- **sonarqube**: Plataforma de análise de código, acessível apenas internamente.
- **db**: Banco de dados PostgreSQL para persistência dos dados do SonarQube.

## Pré-requisitos
- Docker e Docker Compose instalados
- (Opcional) Domínio configurado para o IP da máquina

## Subindo o ambiente de produção
1. Clone o repositório e acesse a pasta do projeto:
   ```bash
   git clone <repo-url>
   cd sonarqube-community
   ```
2. Suba os containers em modo detach:
   ```bash
   docker compose -f docker-compose.prod.yaml up -d
   ```
3. Aguarde alguns minutos até o SonarQube inicializar (primeira vez pode demorar).
4. Acesse via navegador:
   - http://<IP-da-máquina> (ou http://localhost se local)

## Parar o ambiente
```bash
docker compose -f docker-compose.prod.yaml down
```

## Observações
- O Nginx faz proxy para o SonarQube, que só aceita conexões internas.
- O healthcheck garante que o Nginx só tente encaminhar requisições quando o SonarQube estiver pronto.
- Os dados são persistidos em volumes Docker.

## Customização
- Para HTTPS, edite o arquivo `nginx.conf` e adicione certificados SSL.
- Para alterar usuários/senhas, edite as variáveis de ambiente no compose.

---
Dúvidas ou problemas? Abra uma issue!
