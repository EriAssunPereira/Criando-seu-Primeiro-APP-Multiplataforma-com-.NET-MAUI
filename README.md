# Criando-seu-Primeiro-APP-Multiplataforma-com-.NET-MAUI

### Criando seu Primeiro APP Multiplataforma com .NET MAUI

#### DESCRIÇÃO

Neste desafio de projeto, vamos explorar a criação do nosso primeiro aplicativo multiplataforma utilizando o .NET MAUI. O .NET MAUI (Multi-platform App UI) é uma estrutura moderna que permite desenvolver aplicativos nativos para Android, iOS, macOS e Windows utilizando C# e XAML. Com essa poderosa ferramenta, podemos construir aplicativos robustos e adaptáveis a partir de uma única base de código compartilhada.

#### Módulos do Projeto:

1. **Introdução ao .NET MAUI**
   - Visão geral do .NET MAUI como uma estrutura multiplataforma.
   - Benefícios de usar .NET MAUI para desenvolvimento de aplicativos móveis e de área de trabalho.

2. **Configuração do Ambiente**
   - Instalação do .NET MAUI SDK e ferramentas necessárias.
   - Configuração do ambiente de desenvolvimento (Visual Studio ou Visual Studio Code).

3. **Configuração do Dispositivo para Depuração**
   - Configuração do dispositivo Android/iOS para depuração através do Visual Studio.
   - Instalação de emuladores se necessário.

4. **Criação do Projeto .NET MAUI**
   - Criação de um novo projeto .NET MAUI usando modelos disponíveis.
   - Exploração da estrutura do projeto e seus componentes principais.

5. **Desenvolvimento de uma Aplicação Básica**
   - Implementação de uma aplicação básica de gerenciamento de tarefas.
   - Utilização de páginas, layouts e controles adaptáveis.

6. **Teste e Depuração**
   - Teste da aplicação em dispositivos e emuladores.
   - Depuração de problemas comuns e soluções.

7. **Publicação e Distribuição**
   - Opções para publicação do aplicativo em diferentes lojas (Google Play Store, Apple App Store, etc.).
   - Considerações sobre distribuição e atualizações.

#### Conclusão

Ao final deste projeto, estaremos familiarizados com os conceitos essenciais do .NET MAUI e terá desenvolvido seu primeiro aplicativo multiplataforma. Este aprendizado servirá como base sólida para explorar projetos mais avançados e complexos utilizando esta tecnologia moderna e poderosa.

Com este roteiro, poderemos guiar-se passo a passo na criação de um aplicativo multiplataforma com .NET MAUI, garantindo uma compreensão clara desde a configuração do ambiente até a publicação do aplicativo finalizado.

Vamos criar alguns exemplos básicos para ilustrar como seria o desenvolvimento de um aplicativo simples de gerenciamento de tarefas utilizando .NET MAUI. Vou apresentar exemplos de código para criar a interface de usuário e implementar a lógica básica de adicionar e exibir tarefas.

### Exemplo de Interface de Usuário (XAML)

Primeiro, vamos criar a interface de usuário utilizando XAML. Crie um arquivo chamado `MainPage.xaml` dentro da pasta `Pages` do seu projeto .NET MAUI:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:viewModels="clr-namespace:YourAppName.ViewModels"
             x:Class="YourAppName.Pages.MainPage"
             BackgroundColor="{DynamicResource PageBackgroundColor}">
    <ContentPage.Resources>
        <ResourceDictionary>
            <!-- Define estilos e recursos aqui, se necessário -->
        </ResourceDictionary>
    </ContentPage.Resources>

    <StackLayout Padding="20">
        <Entry Placeholder="Digite uma nova tarefa" Text="{Binding NewTaskText}" />
        <Button Text="Adicionar Tarefa" Command="{Binding AddTaskCommand}" />
        
        <ListView ItemsSource="{Binding Tasks}" VerticalOptions="FillAndExpand">
            <ListView.ItemTemplate>
                <DataTemplate>
                    <TextCell Text="{Binding}" />
                </DataTemplate>
            </ListView.ItemTemplate>
        </ListView>
    </StackLayout>
</ContentPage>
```

### Exemplo de ViewModel (C#)

Agora, crie uma classe de ViewModel para a página `MainPage.xaml` dentro da pasta `ViewModels` do seu projeto:

```csharp
using System.Collections.ObjectModel;
using System.Windows.Input;
using Microsoft.Maui.Controls;
using Microsoft.Maui.Controls.Xaml;

namespace YourAppName.ViewModels
{
    public class MainPageViewModel : BindableObject
    {
        private string _newTaskText;
        public string NewTaskText
        {
            get => _newTaskText;
            set
            {
                _newTaskText = value;
                OnPropertyChanged();
            }
        }

        public ObservableCollection<string> Tasks { get; } = new ObservableCollection<string>();

        public ICommand AddTaskCommand { get; }

        public MainPageViewModel()
        {
            AddTaskCommand = new Command(AddTask);
        }

        private void AddTask()
        {
            if (!string.IsNullOrWhiteSpace(NewTaskText))
            {
                Tasks.Add(NewTaskText);
                NewTaskText = string.Empty; // Limpa o texto da entrada
            }
        }
    }
}
```

### Configuração da Página Principal

Por fim, configure a página principal do seu aplicativo para usar `MainPage.xaml` no arquivo `App.xaml.cs`:

```csharp
using Microsoft.Maui;
using Microsoft.Maui.Controls.Hosting;
using Microsoft.Maui.Hosting;

namespace YourAppName
{
    public class MauiProgram
    {
        public static MauiApp CreateMauiApp()
        {
            var builder = MauiApp.CreateBuilder();
            
            builder
                .UseMauiApp<App>()
                .ConfigureMauiHandlers(handlers =>
                {
                    // Configure handlers, if needed
                });

            return builder.Build();
        }
    }

    public partial class App : Application
    {
        public App()
        {
            MainPage = new MainPage();
        }
    }
}
```

### Explicação Rápida dos Exemplos

- **XAML da Página Principal (`MainPage.xaml`)**: Define a interface do usuário com uma entrada para adicionar tarefas, um botão para adicionar tarefas e uma lista de tarefas exibidas.
- **ViewModel (`MainPageViewModel.cs`)**: Contém a lógica de manipulação de dados para adicionar tarefas à lista e é vinculada à página XAML para atualizações de propriedades.
- **Configuração da Aplicação (`App.xaml.cs`)**: Define a página principal do aplicativo como `MainPage`.

Este é um exemplo básico para começar com .NET MAUI. Podemos expandir este projeto adicionando mais funcionalidades, como edição e exclusão de tarefas, estilização avançada da interface do usuário, e integrando serviços externos para persistência de dados, conforme necessário para o seu aplicativo.

