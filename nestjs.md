# NestJs

## Links Úteis
* [Site Oficial](https://nestjs.com/)

## Instalação
```bash
npm i -g @nestjs/cli
```

## Criar um projeto novo
```bash
nest new project-name
```

## Criar recursos pela CLI
```bash
# Gera um módulo de CRUD completo
nest generate resource resource-name

# Gerar um módulo
nest generate mo module-name
```

## Swagger (OpenAPI)
* [Documentação](https://docs.nestjs.com/openapi/introduction)
```bash
# Instalar dependência
npm install --save @nestjs/swagger
```
```javascript
// Adicionar e configurar o Swagger no "main.ts"
async function bootstrap() {
	const app = await NestFactory.create(AppModule);

	const configOpenAPI = new DocumentBuilder()
    	.setTitle('My Resume')
		.setDescription('My Resume App API com NestJs')
		.setVersion('1.0')
		.addTag('my_resume')
		.build();
	const document = SwaggerModule.createDocument(app, configOpenAPI);
	SwaggerModule.setup('swagger-ui', app, document);

	await app.listen(3000);
}
bootstrap();
```
```json
// Habilitando plugin para mapeamento automático, incluindo a configuração no arquivo "nest-cli.json"
"compilerOptions": {
    "plugins": ["@nestjs/swagger"]
}
```
