# Testes de Integração em Flutter

Em Flutter, testes de unidade têm como objetivo verificar o comportamento de ações simples dentro do app, como por exemplo a criação de objetos e os retornos de funções.

Caso se queira testar o comportamento de widgets, ou seja, de componentes mais complexos do aplicativo, são utilizados os testes de widget. 

Mas existe um cenário em que é necessário testar os comportamentos do aplicativo de forma mais ampla e inter-dependente. Por exemplo, em casos onde acontecem atualizações de valores nas "Single source of truths" ou para verificar as interfaces esperadas em uma navegação simulada do usuário.
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