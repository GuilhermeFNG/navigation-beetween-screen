Commit 1: "Passagem de parâmetros obrigatórios na tela de Perfil"
Neste commit, adicionou-se a capacidade de passar um parâmetro obrigatório chamado nome para a tela de Perfil.
Na rota, foi criado o padrão "perfil/{nome}", onde {nome} é um placeholder (marcador) que será preenchido com um valor específico.
Quando o usuário clica no botão "Perfil" do Menu, o código navega assim: navController.navigate("perfil/Fulano de Tal")
Na tela de Perfil, o valor é recuperado com: it.arguments?.getString("nome", "Usuário Genérico")
O parâmetro é obrigatório porque está definido direto na rota (entre chaves {}).
A tela então exibe: "PERFIL - Fulano de Tal"
É como um pacote de correio onde você escreve um endereço ({nome}) e envia a encomenda (perfil/Fulano). O recebedor sabe que aquele pacote é para "Fulano".

Commit 2: "Passagem de parâmetros opcionais na tela de Pedidos"
Adicionou-se a capacidade de passar um parâmetro opcional chamado cliente para a tela de Pedidos usando query string (como em URLs de websites).
A rota foi criada como: "pedidos?cliente={cliente}" (note o ? que indica parâmetros opcionais)
Foram definidas as propriedades do argumento com navArgument(), indicando um valor padrão: "Cliente Genérico"
Quando o usuário clica em "Pedidos", navega-se com: navController.navigate("pedidos?cliente=Cliente XPTO")
Se não houver cliente informado, usa-se o valor padrão automaticamente
A tela exibe: "PEDIDOS - Cliente XPTO"
É como um restaurante onde você pode pedir "sopa de tomate" (obrigatório) ou especificar "com croutons extras" (opcional). Se não especificar, vem o padrão.

Commit 3: "Inserção de valor em parâmetro opcional"
O Menu foi atualizado para enviar um valor específico ao navegar para a tela de Pedidos.
O botão de Pedidos foi modificado de: navController.navigate("pedidos")
Para: navController.navigate("pedidos?cliente=Cliente XPTO")
Agora, sempre que se clica em "Pedidos", a tela já recebe "Cliente XPTO" como parâmetro
A diferença é que antes o parâmetro era opcional (você podia deixar em branco), agora é preenchido automaticamente
É como pré-preencher um formulário. Você já está dizendo "quando ir para Pedidos, mande o cliente XPTO".

Commit 4: "Passagem de múltiplos parâmetros entre telas"
A rota de Perfil foi modificada para aceitar não apenas o nome, mas também a idade como segundo parâmetro obrigatório.
A rota mudou de: "perfil/{nome}"
Para: "perfil/{nome}/{idade}" (dois parâmetros, separados por /)
Foi necessário definir o tipo de cada argumento com NavType:
nome é StringType (texto)
idade é IntType (número inteiro)
Quando navega para Perfil: navController.navigate("perfil/Fulano de Tal/27")
Na tela, recuperam-se ambos os valores:
val nome: String? = it.arguments?.getString("nome")
val idade: Int? = it.arguments?.getInt("idade")
A tela exibe: "PERFIL - Fulano de Tal tem 27 anos"
É como enviar um envelope com várias informações dentro. Ao invés de apenas o nome, agora você está enviando nome E idade separados por barras (/), como em uma URL.