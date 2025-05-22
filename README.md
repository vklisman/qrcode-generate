# QR Code Generator

![Java](https://img.shields.io/badge/Java-17-orange)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.4.4-brightgreen)
![AWS SDK](https://img.shields.io/badge/AWS%20SDK-2.24.12-yellow)
![Google ZXing](https://img.shields.io/badge/Google%20ZXing-3.5.2-blue)
![Docker](https://img.shields.io/badge/Docker-✓-blue)
![Maven](https://img.shields.io/badge/Maven-3.9.6-red)

Uma aplicação Spring Boot que gera códigos QR e os armazena no AWS S3. Este projeto demonstra a integração da biblioteca ZXing do Google para geração de código QR e AWS S3 para armazenamento.

## Como usar

Esta seção fornece instruções abrangentes para configurar e executar a aplicação do Gerador de Código QR.
### Prerequisites

- Java 17 JDK
- Maven
- Docker
- Conta da AWS com acesso ao S3
- AWS CLI configurado com credenciais apropriadas

### Variáveis de Ambiente

Criar um arquivo `.env` na raiz do projeto com as seguintes variáveis:
```env
AWS_ACCESS_KEY_ID=your_access_key
AWS_SECRET_ACCESS_KEY=your_secret_key
AWS_REGION=your_region
AWS_BUCKET_NAME=your_bucket_name
```

### Rodando a Aplicação

#### Desenvolvimento Local

1. Crie o arquivo `.env` conforme descrito acima.
2. Construa o projeto:
   ```bash
   mvn clean package
   ```
3. Rode a aplicação:
   ```bash
   mvn spring-boot:run
   ```

#### Implantação do Docker

1. Construa a imagem do Docker:
   ```bash
   docker build -t qrcode-generator:X.X . 
   ```
> Lembre-se de substituir a versão e o nome da imagem se você quiser

2. Rode o container:
   ```bash
   docker run --env-file .env -p 8080:8080 qrcode-generator:X.X 
   ```

> Lembre-se de substituir o caminho do arquivo .env para o caminho do arquivo de ambiente que você criou.

### Configuração do AWS S3

1. Criar um bucket do S3 na sua conta da AWS
2. Atualize o comando `AWS_BUCKET_NAME` no seu arquivo `.env` ou no comando Docker run
3. Certifique-se de que suas credenciais da AWS tenham permissões apropriadas para acessar o bucket do S3

## API Endpoints

### POST /qrcode
Gera um código QR a partir do texto fornecido e armazená-lo no AWS S3. O código QR será gerado como uma imagem PNG com dimensões de 200x200 pixels.
**Parameters**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `text` | required | string | Conteúdo do texto a ser codificado no código QR. Este pode ser qualquer valor de string que você deseja converter em um código QR. |

**Response**

```json
{
    "url": "https://your-bucket.s3.your-region.amazonaws.com/random-uuid"
}
```

**Resposta de erro**

Se ocorrer um erro durante a geração de código QR ou o upload do S3, a API retornará um erro de servidor interno de 500.
**Examplo de uso:**

```bash
curl -X POST http://localhost:8080/qrcode \
     -H "Content-Type: application/json" \
     -d '{"text": "https://example.com"}'
```

## Licença

Este projeto está licenciado sob a Licença MIT - consulte o arquivo LICENSE para obter detalhes.