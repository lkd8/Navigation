Documentação: Checkpoint 1 - Navigation Compose
1. Descrição do Projeto
   O projeto consiste em uma aplicação Android desenvolvida com Jetpack Compose que demonstra a transição entre múltiplas telas (Menu, Pedidos, Perfil) utilizando a biblioteca Navigation Compose. O foco central desta etapa foi a implementação de fluxos de dados dinâmicos através da passagem de parâmetros entre rotas.

2. Objetivo da Prova
   Avaliar a capacidade de evolução incremental de um software, aplicando conceitos avançados de navegação, como parâmetros obrigatórios, opcionais (query strings) e tipagem de dados.

3. Explicação das Evoluções Implementadas
   3.1. Passagem de Parâmetros Obrigatórios (Tela de Perfil)

O que foi implementado: A rota de Perfil deixou de ser estática e passou a exigir um nome para ser acessada.

Configuração da Navegação: Na MainActivity.kt, a rota foi definida como "perfil/{nome}". O uso de chaves {} indica que este segmento da URL é um argumento variável.

Envio de Parâmetros: No MenuScreen.kt, o navController.navigate agora envia uma string formatada: "perfil/Fulano de Tal".

Recebimento de Parâmetros: Dentro do NavHost, recuperamos o valor através de it.arguments?.getString("nome"). Este valor é então repassado para a função @Composable PerfilScreen, que o utiliza para exibir um título personalizado: "PERFIL - $nome".

3.2. Passagem de Parâmetros Opcionais (Tela de Pedidos)

O que foi implementado: Implementação de navegação que não exige obrigatoriamente um dado para funcionar, utilizando o conceito de Query Parameters.

Configuração da Navegação: A rota foi configurada como "pedidos?cliente={cliente}". O símbolo ? diferencia este parâmetro de um obrigatório.

Valor Padrão: Foi utilizado o navArgument("cliente") com um defaultValue = "Cliente Genérico". Isso garante que, se a tela for chamada sem argumentos, o app não apresente erro e exiba um valor padrão.

Recebimento: O parâmetro é extraído de forma nula (String?) e repassado para a PedidosScreen.

3.3. Inserção de Valor ao Parâmetro Opcional

O que foi implementado: Ativação do envio de dados na rota de pedidos através da interface de usuário.

Configuração: No MenuScreen.kt, o clique do botão foi atualizado para navegar especificamente para "pedidos?cliente=Cliente XPTO".

Funcionamento: Ao realizar essa chamada, o Navigation substitui o valor padrão configurado anteriormente pelo valor explícito enviado ("Cliente XPTO"), demonstrando a flexibilidade entre parâmetros padrão e dinâmicos.

3.4. Passagem de Múltiplos Parâmetros

O que foi implementado: Extensão da tela de Perfil para aceitar e processar mais de um dado simultaneamente, incluindo tipagem numérica.

Configuração e Tipagem: A rota evoluiu para "perfil/{nome}/{idade}". Na MainActivity.kt, definimos explicitamente o tipo do segundo argumento como NavType.IntType. Isso é crucial para que o sistema de navegação converta automaticamente a String da URL em um Inteiro.

Envio: O MenuScreen.kt envia os dados concatenados: "perfil/Fulano de Tal/27".

Recebimento e Exibição: A PerfilScreen foi modificada para receber ambos os parâmetros (nome: String, idade: Int). O resultado visual foi atualizado para exibir uma frase composta: "PERFIL - $nome tem $idade anos".