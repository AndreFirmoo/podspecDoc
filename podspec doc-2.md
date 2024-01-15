# Guia de configuração do podspec

  

# Índice

1. Podspec padrão vindo da AA. 
	2. Explicando as propriedades.
2. Boas praticas.
3. Implementando as boas praticas.

## Podspec vindo da AA
Quando implementamos o plugin de modulo do AA recebemos o podspec dessa forma:
```ruby
Pod::Spec.new do |s|
	s.name = 'Toturial'
	s.version = '0.1.0'
	s.summary = 'A short description of Toturial.'
	s.description = <<-DESC
	TODO: Add long description of the pod here.
	DESC
	s.homepage = 'https://github.com/Toturial/Toturial'
	s.license = { :type => 'MIT', :file => 'LICENSE' }
	s.author = { 'Toturial' => 'email2@example.com' }
	s.source = { :git => 'https://github.com/Toturial/Toturial.git', :tag => s.version.to_s }
	s.ios.deployment_target = '11.0'
	s.source_files = 'Toturial/Classes/**/*'
end
```

É uma implementação base criada para adiantar o nosso processo de criar isso manualmente. Abaixo tem exemplo de propriedades opcionais e obrigatória a implementação.

 
- [x] propriedade obrigatória
- [ ] propriedade opcional

### Propriedades.
 #### Name
Quando colocamos o nome do modulo no AA automaticamente inclui na propriedade ```s.name``` o nome do seu pod na propriedade.


**Propriedade name** 
- [x] **name**: **String** - Nome do seu Pod, esse mesmo nome que irá usar para colocar no podfile de um projeto.
```ruby
s.name = 'NomeDoPod'
```

#### Version
Incluindo a versão do seu pod. É recomendado utilizar o [Semantic Versioning (e.g., MAJOR.MINOR.PATCH).](https://semver.org)

**Propriedade version**
- [x] **version**: **String** - Versão do Pod. Com essa versão ira ser incluída após o nome do pod.
```ruby
s.version = '0.1.0'
```

#### Summary
Aqui onde deve-se fazer a inclusão de um resumo sobre o que seu pod se trata. 

**Propriedade summary**
- [x] **summary**: **String** - Onde irá incluir um breve resumo sobre seu Pod.
```ruby
s.summary = 'Resumo do seu pod'
```
#### Description
Aqui onde é opcional a inclusão de uma descrição simples sobre o que seu pod se trata. 
> Entretanto recomendo a inclusão dessa informação para facilitar o entendimento sobre o que esse pod faz.

**Propriedade description**
- [ ] **description**:**String** - Pode-se fazer com string ou heredoc.

```ruby
s.description = 'descrição do seu pod.'
```
Ou
```ruby
s.description = <<-DESC
	Aqui pode ser uma descrição pelo heredoc.
DESC
```

#### Homepage
A URL da página principal do pod, geralmente onde o código-fonte pode ser encontrado.

**Propriedade homepage**
- [x] **homepage**: **String** - A URL do git.


#### License
A propriedade `license` é usada para definir a licença sob a qual o pod é distribuído. Esta propriedade é importante pois especifica como o pod pode ser usado, modificado e distribuído.

- [x] **license**: **hash** - Neste hash, você pode especificar detalhes sobre a licença do seu pod.
	- [x] **:type**: **String** - Uma string que especifica o tipo da licença. Por exemplo, `'MIT'`, `'Apache'`, `'GPL'`, etc.
	- [ ] **:file**: **String** - Uma string que fornece o caminho para o arquivo de licença no repositório do pod. Geralmente, este é um arquivo chamado `LICENSE` ou algo semelhante.
	- [ ] **:text**: **String** - Uma string que contém o texto completo da licença. Esta opção é menos comum, pois a maioria dos projetos prefere referenciar um arquivo de licença externo.

```ruby
	s.license = { :type => 'MIT', :file => 'LICENSE' }
```

#### Author
A propriedade ```s.author``` é usada para definir os autores do time que atuam pod, facilidando assim a identificação dos desenvolvedores.

- [x] **author**: **hash** | **Array** | **String** - Pode receber um dentre esses para definir o Autor do pod.

Essa propriedade pode ser definida de varias formas diferentes, dentre elas são.:
1. **Autor Único:** Se o pod tem apenas um autor, você pode definir `s.author` com o nome do autor e o endereço de e-mail em um hash. Por exemplo.:
```ruby
s.author = { 'Nome do Autor' => 'email@example.com' }
```
2. **Vários Autores:** Para múltiplos autores, você pode expandir o hash para incluir cada autor e seu respectivo e-mail. Por exemplo.:
```ruby
s.authors = { 
'Autor 1' => 'email1@example.com', 
'Autor 2' => 'email2@example.com' 
}
```
3. **Somente Nomes:** Se você preferir não incluir os endereços de e-mail, você pode simplesmente fornecer os nomes dos autores em um array. Por exemplo.:
```ruby
s.authors = ['Autor 1', 'Autor 2']
```

4. **Utilizando String:** Em alguns casos, especialmente quando há apenas um autor, você pode optar por usar uma string simples. Este método é menos comum e geralmente não inclui o endereço de e-mail. Por exemplo.:
```ruby
s.author = 'Nome do Autor'
```

A forma mais comum e recomendada é usar um hash com nomes e endereços de e-mail, pois isso fornece clareza e facilita o contato. É importante fornecer informações precisas e atualizadas sobre os autores, pois isso ajuda outros desenvolvedores a identificar quem são os principais contribuintes do pod e como entrar em contato com eles para colaborações, questões ou feedback.

#### Source
A propriedade `s.source` é usada para indicar a origem do código-fonte do pod. Essa informação é crucial, pois define de onde o CocoaPods deve buscar o código quando o pod é incluído em um projeto.

- [x] **source**: **hash**
##### Utilizando o git como origin do codigo fonte.: 
- [x] **:git**: **String** - URL do repositório 
- [ ] **:tag**: **String** - Tag da versão
- [ ] **:commit**: **String** - Hash do commit
```ruby
s.source = { :git => 'https://github.com/Example/ExamplePod.git', :tag => s.version.to_s }
	Ou
s.source = { :git => 'https://github.com/Example/ExamplePod.git', :commit => 'abcd1234' }
```
##### **HTTP (Arquivo Zip/Tar):** Para um arquivo hospedado em um servidor HTTP (como um arquivo .zip ou .tar), use a chave `:http`.:
- [x] **:http**: **String** - URL onde o arquivo .zip ou .tar está armazenado.
```ruby
s.source = { :http => 'https://example.com/ExamplePod.zip'}
```
> Note: É recomendado utilizar a chave ```:http``` para pegarmos direto do arti
##### **Path (Local):** Para desenvolvimento local ou testes, você pode especificar um caminho local usando a chave `:path`.:
- [x] **:path**: **String** - Caminho do local onde se encontra o source.

```ruby
s.source = { :path => '~/path/to/ExamplePod' }
```

> Note: Esta abordagem é geralmente usada apenas para desenvolvimento local, não para pods que serão distribuídos publicamente.


#### Plataform deployment target

A propriedade ```s.ios.deployment_target``` especifica a versão mínima que seu pod irá rodar no iOS. 

- [x] **s.ios.deployment_target**: **String** - Especifica a versão mínima do pod.

> Note: Existem outras plataformas da apple que usam algo semelhante. Basta apenas trocar o ```s.ios``` pela plaforma desejada, por exemplo.: ```s.osx``` para criar uma versão mínima para o macOS.

#### Source Files
A propriedade ```s.source_files``` especifica onde estará os arquivos utilizados no desenvolvimento do seu pod.

> Note: Cuidado, a raiz vai ser onde o podspec estiver, quando colocar as informações tome cuidado ao referenciar os arquivos e pastas.

Aqui estão algumas formas comuns de usar `s.source_files`.:

1.  **Caminho Direto para Arquivos Individuais:** Você pode listar os caminhos para arquivos específicos, separados por vírgulas. Exemplo:
  ```ruby 
  s.source_files =  'Classes/MyClass1.swift',  'Classes/MyClass2.swift'
  ```
    
2.  **Coringas para Múltiplos Arquivos:** Para incluir todos os arquivos de um tipo específico em um diretório, você pode usar coringas (`*`). Exemplo:
   ```ruby
    s.source_files =  'Classes/*.swift'   
   ```
>    Note: Isso incluirá todos os arquivos `.swift` no diretório `Classes`.
    
3.  **Coringas para Subdiretórios:** Você pode usar `**` para incluir arquivos em um diretório e todos os seus subdiretórios. Exemplo:
```ruby 
s.source_files =  'Classes/**/*.swift'
```
    
>Note: Isso incluirá todos os arquivos `.swift` dentro do diretório `Classes` e em qualquer subdiretório dentro dele.
    
4.  **Múltiplos Padrões:** Você também pode combinar vários padrões em uma única string, usando chaves `{}` para agrupar os padrões. Exemplo:
```ruby
s.source_files =  'Classes/**/*.{h,m,swift}'
```   
>Note: Isso incluirá todos os arquivos `.h`, `.m`, e `.swift` no diretório `Classes` e seus subdiretórios.

Outras propriedades que não vem por padrão quando criamos um modulo pode ser consultada na [referencia de sintaxe do podspec](https://guides.cocoapods.org/syntax/podspec.html#specification).

### Boas práticas

#### Informações 
Por mais que exista o readMe dentro do projeto, é importante deixar as informações de resumo, descrição e autores detalhadas, a fim de facilitar o contato.

#### Organização de pastas
Ajustar aqui amanha

#### Criação dos subspecs
A criação de subspecs é essencial para organização e manutenção do seu pod. 
Os subspecs podem variar conforme a necessidade.
> Note: Entretanto é necessario ter esses.: 
	Debug -> Onde é usado no momento de desenvolvimento. Colocamos os ```source_files```, ```resource``` , etc... 
	Tests -> Define quais arquivos estaram disponível para ser executado no target de testes.
	Release -> Onde definimos o XCFramework e configuração de xcconfig do pod para rodar em produção.

##### Debug
```ruby
s.subspec 'Debug' do |debug| 
	debug.source_files = 'seuPod/Classes/**/*'
	debug.resources = 'seuPod/Assets/**/*.{.xib, .jpg,.json}'
end
```

##### Tests
```ruby
s.subspec 'Tests' do |tests| 
	tests.source_files = 'seuPod/Tests/**/*'
	tests.resources = 'seuPod/Tests/**/*.{.xib, .jpg,.json}'
end
```

##### Release
```ruby
s.subspec 'Release' do |release| 
	release.vendored_frameworks = 'SeuNomePod.framework'
end
```

##### Podspec com essas configurações.: 

```ruby
Pod::Spec.new  do |s|
	s.name =  'PodExemple'
	s.version =  '0.1.0'
	s.summary =  'Esse projeto é apenas para fins de exemplo.'
	s.description =  <<-DESC
		A proposta desse projeto é disseminar um pouco de conhecimento.
	DESC
	s.homepage =  'https://github.com/repo/PodExemple'
	s.license = { :type => 'MIT', :file => 'LICENSE' }
	s.author = { 'Andre' => 'seuemail@mail.com' }
	s.source = { :git => 'https://github.com/repo/PodExemple.git', :tag => 	s.version.to_s }
	s.ios.deployment_target =  '11.0'
	
	s.default_subspecs =  'Release'
	
	s.subspec 'Debug'  do |debug|
		debug.source_files =  'PodExemple/Classes/**/*'
		debug.resources =  'PodExemple/Assets/**/*.{.xib, .jpg,.json}'
		debug.resource_bundles = {
		'PodExemple' => ['PodExemple/Assets/*.png']
		}
		debug.subspec 'Tests'  do |tests|
			tests.source_files =  'PodExemple/Tests/**/*'
			tests.resources =  'PodExemple/Tests/**/*.{.xib, .jpg,.json}'
			end
		end
		
	s.subspec 'Release'  do |release|
		release.vendored_frameworks =  'PodExempleframework'
	end
end
```

##### Testando seu pod no app sample

Para testar em desenvovimento seu pod é muito fácil, basta ir no arquivo podfile do seu sample e colocar dessa forma.: 

```ruby
pod 'PodExemple/Debug', :path => '../' , :testspecs => ['Tests']
```
> Note: A chave ```:path``` deve colocar o diretório onde encontra o podspec do seu modulo.
 A chave ```:testspecs``` irá buscar nas configurações do seu podspec um subspec com o nome de 'Tests' para testes.

No Xcode deve ficar semelhante a isso: 
TODO: Colocar a imagem de como deve-se ficar

