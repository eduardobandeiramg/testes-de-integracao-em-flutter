# Testes de Integração em Flutter

Em Flutter, testes de unidade têm como objetivo verificar o comportamento de ações simples dentro do app, como por exemplo a criação de objetos e os retornos de funções.

Caso se queira testar o comportamento de widgets, ou seja, de componentes mais complexos do aplicativo, são utilizados os testes de widget. 

Mas existe um cenário em que é necessário testar os comportamentos do aplicativo de forma mais ampla e inter-dependente. Por exemplo, em casos onde é preciso verificar as interfaces esperadas e comportamentos ao longo de uma navegação simulada do usuário. Além disso, testes de integração também são úteis quando se deseja verificar e validar os valores que estão sendo armazenados na "single source of truth" quando se está usando gerenciamento de estado.
Nesses casos, onde se faz uso de alguma forma de gerenciamento de estados, é necessário usar *testes de integração*.

## Como fazer testes de integração

1. Adicionar as dependências
Adicionar as dependências de "integration_test" no arquivo pubspec.yaml

```yaml
dev_dependencies:
  flutter_test:
    sdk: flutter

  integration_test:
    sdk: flutter
```

2. Criar uma pasta para os testes de integração na raiz do projeto (Deve conter a palavra 'test'. Exemplo: "integration_test")
3. Criar um arquivo para cada teste de integração:

```dart
import 'package: integration_test/integration_test.dart';
import 'main' as app;

void main(){
  IntegrationTestWidgetsFlutterBinding.ensureInitialized();
  
  testWidgets("descricao"(WidgetTester tester) async {
    app.main(); // Executa o app
    await tester.pumpAndSettle();
    await tester.tap(finder.text("nome_botao"));
    await tester.pumpAndSettle();
    ...
    ...
    ...
  });
}
```

Observação: para se verificar valores do ChangeNotifier quando se usa o gerenciador de estado Provider, é necessário criar uma chave para que se possa recuperar o valor do contexto do app.

```dart
import 'package: integration_test/integration_test.dart';
import 'main' as app;

void main(){
  IntegrationTestWidgetsFlutterBinding.ensureInitialized();
  
  testWidgets("descricao"(WidgetTester tester) async {
    chave = GlobalKey();
    app.main([], chave); // Executa o app
    await tester.pumpAndSettle();
    await tester.tap(finder.text("nome_botao"));
    await tester.pumpAndSettle();
    ...
    ...
    ...
  });
}
```
